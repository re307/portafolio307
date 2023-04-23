<!-- 
<div id="menu" class="container">
    <div id="temporizador" class="timer">00:00</div>
    <div id="reinicio">boton reincio</div>
    <div id="contador" class="timer">00</div>
</div>
<div id="contenedor" class="container">
</div>
<style>
    #menu{
      display: grid;
      grid-template-columns: repeat(3, 0.5fr);
      background-color: rgb(97, 148, 20);
      height: 50px;
    }
    .container{
      display: grid;
      grid-template-columns: repeat(18, 0fr);
      /* grid-auto-rows: 100px; */
      /* grid-gap: 20px; */
    }
    .timer{
      width: 100px;
      height: 35px;
      margin-top: 9px;
      margin-bottom: 1px;
      margin-left: 1px;
      margin-right: 1px;
      background-color: #030202;
      color: red;
    }
    #temporizador{
      margin-left: 30px;
      text-align: center;
    }
    #contador{
      margin-left: 40px;
      text-align: center;
    }
</style>
<script>
    import { onMount } from 'svelte';
    onMount(()=>{
        class Celda{
            numero = 0;
            div;
            pasos = new Array();
            alto = 0;
            bajo = 252;
            lateral = 18;
            esBomba = false;
            aparturada = false;
            cercania = 0;
            constructor(numero,esBomba = false){
                this.numero = numero;
                this.esBomba = esBomba;
                this.cercania =(esBomba?20:0);
                this.div = document.createElement('div');
                this.div.id = `celda${numero}`;
                this.div.className = 'celda';
                this.div.innerHTML = `<div style="display:none">${(this.esBomba?`<img src="${""}" class="logo" alt="Vite logo" />`:`<p>${this.cercania.toString()}</p>`)}</div>`;
                for (let paso = 1; paso <= 8; paso++) {
                let operacion = 0
                let borde = (numero%this.lateral<2?(true):false);
                let bordeDerecho = (borde?(numero%this.lateral==0?true:false):false);
                let bordeIzquierdo = (borde?(numero%this.lateral==1?true:false):false);
                switch (paso) {
                    case 1:
                    if ((numero-1)>0&&!bordeIzquierdo) {
                        this.pasos.push(numero-1)
                    }
                    break;
                    case 2: 
                    if ((numero+(this.lateral-1))<this.bajo&&!bordeIzquierdo) {
                        this.pasos.push(numero+(this.lateral-1))
                    }
                    break;
                    case 3:
                    if ((numero+this.lateral)<this.bajo) {
                        this.pasos.push(numero+this.lateral)
                    }
                    break;
                    case 4:
                    if ((numero+(this.lateral+1))<this.bajo&&!bordeDerecho) {
                        this.pasos.push(numero+(this.lateral+1))
                    }
                    break;
                    case 5:
                    if ((numero+1)<this.bajo&&!bordeDerecho) {
                        this.pasos.push(numero+1)
                    }
                    break;
                    case 6:
                    if ((numero-(this.lateral-1))>this.alto&&(bordeIzquierdo||!borde)) {
                        this.pasos.push(numero-(this.lateral-1))
                    }
                    break;
                    case 7:
                    if ((numero-this.lateral)>0) {
                        this.pasos.push(numero-this.lateral)
                    }
                    break;
                    case 8:
                    operacion = numero-(this.lateral+1);
                    if ((numero-(this.lateral+1))>this.alto&&(bordeDerecho||!borde)) {
                        this.pasos.push(numero-(this.lateral+1))
                    }
                    break;
                    default:
                    break;
                }
                }
            }
            setCercania(){
                if (!this.esBomba) {
                this.cercania++;
                } 
                this.div.innerHTML = `<div style="display:none">${(this.esBomba?`<img src="${""}" class="logo" alt="Vite logo" />`:`<p>${this.cercania.toString()}</p>`)}</div>`;
            }
            setAperturada(){
                this.aparturada = true;
            }
        }
        let tablero = new Array();
        let celdasBombas = new Array();
        const metaBuscaminas =(contenedorElement)=>{
            let totalCeldas = 252;
            let totalBombas = Math.round(totalCeldas / 8);
            for (let index = 1; index <= totalBombas; index++) {
                let celdaBomba = Math.floor(Math.random() * totalCeldas) + 1;
                celdasBombas.push(celdaBomba);
            }
            // console.log(celdasBombas);
            for(let i = 1; i <= totalCeldas;i++){
                let bomba = false; 
                if (celdasBombas.includes(i)) {
                    bomba = true;
                }
                tablero.push(new Celda(i,bomba))
            }
            // console.log(tablero);
            tablero.forEach((value)=>{
                if (value.esBomba) {
                value.pasos.forEach((vecina)=>{
                    tablero[vecina-1].setCercania();
                });
                }
            });
            tablero.forEach((value,index)=>{
                contenedorElement.insertAdjacentHTML('beforeend',value.div.outerHTML);
                document.getElementById(value.div.id).addEventListener('click',()=>{
                let info = {
                    indicador:index,
                    id:value.div.id,
                    vecinas:value.pasos
                }
                cambiaEstatus(info);
                });
            });
        }

        const cambiaEstatus = (info)=>{
            let color = selectorColor(tablero[info.indicador].cercania);
            tablero[info.indicador].setAperturada();

            if (tablero[info.indicador].cercania == 0) {
                document.getElementById(info.id).className = 'celda_libre';
                for (let index = 0; index < info.vecinas.length; index++) {
                let vecina = info.vecinas[index];
                if (tablero[vecina-1].cercania != 0){
                    let elementoDescubrir = document.getElementById(`celda${vecina}`);
                    elementoDescubrir.className = 'celda_libre';
                    elementoDescubrir.childNodes[0].style.display = "block";
                    color = selectorColor(tablero[vecina-1].cercania);
                    elementoDescubrir.childNodes[0].childNodes[0].style.color = color;
                }else{
                    if (tablero[vecina-1].cercania == -1) {
                    
                    } else {
                    if (!tablero[vecina-1].aparturada) {
                        setTimeout(()=>{
                        document.getElementById(`celda${vecina}`).click();
                        },1);
                        
                    }
                    }
                }
                }
            }else{
                if (!tablero[info.indicador].esBomba) {
                document.getElementById(info.id).className = 'celda_libre';
                document.getElementById(info.id).childNodes[0].style.display = "block";
                if (color !== '') {
                    document.getElementById(info.id).childNodes[0].childNodes[0].style.color = color;
                }
                } else {
                celdasBombas.forEach((value)=>{
                    document.getElementById(`celda${value}`).className = 'celda_libre';
                    document.getElementById(`celda${value}`).childNodes[0].style.display = "block";
                });
                document.getElementById('contenedor').classList.add('elementor-toggle');
                document.getElementById("reinicio").addEventListener('click',()=>{
                    document.getElementById("contenedor").innerHTML = '';
                    document.getElementById("contenedor").className = 'container';
                    metaBuscaminas(document.getElementById("contenedor"));
                });
                // var todos = document.getElementById('contenedor').getElementsByTagName('div');
                // for (var node of todos) {
                //     node.disabled = true;
                // }
                }
            }
        }
        const selectorColor = (cercania)=>{
            let color = '';
            switch (cercania) {
                case 0:
                break;
                case 20:
                break;
                case 1:
                    color = "blue";
                break;
                case 2:
                    color = "green";
                break;
                case 3:
                    color = "yellow";
                break;
            
                default :
                    color = "red";
                break;
            }
            return color;
        }
        metaBuscaminas(document.querySelector('#contenedor'))
    });

    // metaBuscaminas(document.querySelector('#contenedor'))
</script> -->