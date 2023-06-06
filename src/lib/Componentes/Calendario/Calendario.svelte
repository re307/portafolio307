<script>
    import { compute_slots } from 'svelte/internal';
    import './calendario.css'
    import Celda from './Celda.svelte'
    const fechaActual = new Date();
    let infoImprimir = new Array();
    let construye = 1;
    let anosSumados = 12;
    const mesesNombre = ["ENE","FEB","MAR","ABR","MAY","JUN","JUL","AGO","SEP","OCT","NOV","DIC"];
    let etiqueta = '';
    let etiquetaCambiad = '';
    let mesInicial = fechaActual.getMonth()+1;
    let anoInicial = fechaActual.getFullYear();
    const mesActual = fechaActual.getMonth()+1;
    const anoActual = fechaActual.getFullYear();
    let mes = fechaActual.getMonth()+1;
    let ano = fechaActual.getFullYear();
    let mesArray = (mesVisual_A)=>{
        infoImprimir = new Array();
        let styleS = null;
        let mesPintar_A;
        let mesNumero_A = mesVisual_A;
        if (mesNumero_A == 13) {
            mesNumero_A = 1;
            mesInicial = 1;
            ano = ano + 1 ;
        }
        if (mesNumero_A == 0) {
            mesNumero_A = 12;
            mesInicial = 12;
            ano=ano-1;
        }
        mesPintar_A = new Date(`${ano}-${mesNumero_A}-01 00:00:00`);
        mesPintar_A.setDate(mesPintar_A.getDate()-mesPintar_A.getDay());
        for (let index = 0; index < 42; index++) {
            if (mesPintar_A.toDateString() === fechaActual.toDateString()) {
                styleS = "dia_actual";
            }else{
                styleS = "dia_libre";
            }
            infoImprimir.push(`<div class="${styleS}">${mesPintar_A.getDate()}</div>`);
            mesPintar_A.setDate(mesPintar_A.getDate()+1);
        }
    }
    let mesesArray = (ano)=>{
        infoImprimir = new Array();
        let styleS = null;
        for (let index = 0; index < 12; index++) {
            if (mesActual === index&&anoActual === ano) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            infoImprimir.push(`<div class="${styleS}"><p>${mesesNombre[index]}</p></div>`);
        }
    }
    let anoArray = (ano)=>{
        infoImprimir = new Array();
        let styleS = null;
        let anoS = `${ano}`;
        let disminucion = Number(anoS[anoS.length-1])+1;
        let inicio = ano - disminucion;
        etiquetaCambiad = `${inicio+1} al ${(inicio+anosSumados)}`
        for (let index = inicio; index < (inicio+anosSumados); index++) {
            if (anoActual ===index) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            infoImprimir.push(`<div class="${styleS}"><p>${index}</p></div>`);
        }
    }
    let cambioHorizontal = (construye,mov)=>{
        switch (construye) {
            case 1:
                console.log("mesInicial: ",mesInicial);
                switch (mov) {
                    case 1:
                        mesInicial=mesInicial+1;
                        mesArray(mesInicial);
                        etiqueta = mesesNombre[mesInicial-1]
                        break;
                    case 0:
                        mesInicial=mesInicial-1;
                        mesArray(mesInicial);
                        etiqueta = mesesNombre[mesInicial-1]
                        break;
                    default:
                        break;
                }
                break;
            case 2:
                switch (mov) {
                    case 1:
                        anoInicial=anoInicial+1;
                        break;
                    case 0:
                        anoInicial=anoInicial-1;
                        break;
                    default:
                        break;
                }
                mesesArray(anoInicial);
                etiqueta = `${anoInicial}`
                break;
            case 3:
                switch (mov) {
                    case 1:
                        anoInicial=anoInicial+anosSumados;
                        break;
                    case 0:
                        anoInicial=anoInicial-anosSumados;
                        break;
                    default:
                        break;
                }
                anoArray(anoInicial);
                etiqueta = `${etiquetaCambiad}`
                break;
        
            default:
                break;
        }
    }
    let selecionaCalenHijo =()=>{
        switch (construye) {
            case 1:
                mesArray(mes);
                etiqueta = mesesNombre[mes-1]
                break;
            case 2:
                mesesArray(ano);
                etiqueta = `${ano}`
                break;
            case 3:
                anoArray(ano);
                etiqueta = `${etiquetaCambiad}`
                break;
        
            default:
                break;
        }
    }
    let selecionaCalen = ()=>{
        construye = (construye<3?construye+1:construye);
        switch (construye) {
            case 1:
                //document.getElementById("calenAno").outerHTML = "";
                mesArray(mes);
                etiqueta = mesesNombre[mes-1]
                break;
            case 2:
                //document.getElementById("calenMes").outerHTML = "";
                mesesArray(ano);
                etiqueta = `${ano}`
                break;
            case 3:
                //document.getElementById("calenMeses").outerHTML = "";
                anoArray(ano);
                etiqueta = `${etiquetaCambiad}`
                break;
            default:
                break;
        }
    }
    switch (construye) {
        case 1:
            mesArray(mes);
            etiqueta = mesesNombre[mes-1]
            break;
        case 2:
            mesesArray(ano);
            etiqueta = `${ano}`
            break;
        case 3:
            anoArray(ano);
            etiqueta = `${etiquetaCambiad}`
            break;
    
        default:
            break;
    }
</script>
<div class="container sinpadding">
    <div class="row">
        <div class="col-sm-4 previo btn-cand" on:click={()=>{cambioHorizontal(construye,0)}}>Previo</div>
        <div class="col-sm-4 muestraInfoDe btn-cand" on:click={()=>{selecionaCalen();}}>{@html etiqueta}</div>
        <div class="col-sm-4 siguiente btn-cand" on:click={()=>{cambioHorizontal(construye,1)}}>Siguiente</div>
    </div>
    <div class="row">
        {#if construye === 1}
            <div class="dia">do.</div>
            <div class="dia">lu.</div>
            <div class="dia">ma.</div>
            <div class="dia">mi.</div>
            <div class="dia">ju.</div>
            <div class="dia">vi.</div>
            <div class="dia">sa.</div>
            <div class="gridMes col-sm-12">
                {#each infoImprimir as data,i }
                    {@html data}
                {/each}
            </div>
        {/if}
        {#if construye === 2}
            <div class="gridMesesAno col-sm-12" id="calenMeses">
                {#each infoImprimir as data,i }
                    {@html data}
                {/each}
            </div>
        {/if}
        {#if construye === 3}
            <div class="gridMesesAno col-sm-12" id="calenAno">
                {#each infoImprimir as data,i }
                    {@html data}
                {/each}
            </div>
        {/if}
    </div>
</div>