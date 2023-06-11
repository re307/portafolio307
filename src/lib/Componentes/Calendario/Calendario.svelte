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
    let mesInicial = fechaActual.getMonth();
    let anoInicial = fechaActual.getFullYear();
    const mesActual = fechaActual.getMonth();
    const anoActual = fechaActual.getFullYear();
    let fechaSelect = null;
    let mes = fechaActual.getMonth();
    let ano = fechaActual.getFullYear();
    let mesArray = (mesVisual_A)=>{
        infoImprimir = new Array();
        mesInicial = mesVisual_A;
        let styleS = null;
        let mesPintar_A;
        let mesNumero_A = mesVisual_A;
        if (mesNumero_A == 12) {
            mesNumero_A = 0;
            mesInicial = 0;
            ano = ano + 1 ;
        }
        if (mesNumero_A == -1) {
            mesNumero_A = 11;
            mesInicial = 11;
            ano=ano-1;
        }
        mesPintar_A = new Date(`${ano}-${mesNumero_A+1}-01 00:00:00`);
        mesPintar_A.setDate(mesPintar_A.getDate()-mesPintar_A.getDay());
        for (let index = 0; index < 42; index++) {
            if (mesPintar_A.toDateString() === fechaActual.toDateString()) {
                styleS = "dia_actual";
            }else{
                if (mesPintar_A.getMonth() == mesNumero_A) {
                    if ((fechaSelect !== null)&&(mesPintar_A.toDateString() === fechaSelect.toDateString())) {
                        styleS = "dia_actual_select";
                    }else{
                        styleS = "dia_libre";
                    }
                }else{
                    styleS = "dia_libre_fuera";
                }
            }
            let info = {
                "style":styleS
                ,"imprimir":mesPintar_A.getTime()
                ,"dia":mesPintar_A.getDate()
            }
            infoImprimir.push(info);
            mesPintar_A.setDate(mesPintar_A.getDate()+1);
        }
    }
    let mesesArray = (ano_Select)=>{
        infoImprimir = new Array();
        ano = ano_Select;
        let styleS = null;
        for (let index = 0; index < 12; index++) {
            if (mesActual === index&&anoActual === ano) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            let diaInical = new Date(`${ano}-${index+1}-01 00:00:00`);
            let info = {
                "style":styleS
                ,"imprimir":mesesNombre[index]
                ,"dia":diaInical.getTime()
            }
            infoImprimir.push(info);
        }
    }
    let anoArray = (ano_Select)=>{
        infoImprimir = new Array();
        ano = ano_Select;
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
            let diaInical = new Date(`${index}-01-01 00:00:00`);
            let info = {
                "style":styleS
                ,"imprimir":index
                ,"dia":diaInical.getTime()
            }
            infoImprimir.push(info);
        }
    }
    let cambioHorizontal = (construye,mov)=>{
        switch (construye) {
            case 1:
                console.log("mesInicial: ",mesInicial);
                switch (mov) {
                    case 1:
                        mesInicial=mesInicial+1;
                        break;
                    case 0:
                        mesInicial=mesInicial-1;
                        break;
                    default:
                        break;
                }
                mesArray(mesInicial);
                if (anoActual == ano) {
                    
                    etiqueta = mesesNombre[mesInicial]
                    
                } else {
                    etiqueta = `${ano}-`+ mesesNombre[mesInicial]
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
    let selecionaCalen = ()=>{
        construye = (construye<3?construye+1:construye);
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
    let celdaSeleccionada = (divInfo,calendario)=>{
        fechaSelect = new Date(divInfo);
        construye = (construye>1?construye-1:construye);
        switch (construye) {
            case 1:
                let mes_S = fechaSelect.getMonth();
                mesArray(mes_S);
                if (anoActual == fechaSelect.getFullYear()) {
                    
                    etiqueta = mesesNombre[mes_S]
                    
                } else {
                    etiqueta = `${fechaSelect.getFullYear()}-`+ mesesNombre[mes_S]
                }
                break;
            case 2:
                let ano_S = fechaSelect.getFullYear();
                mesesArray(ano_S);
                etiqueta = `${ano_S}`
                break;
            // case 3:
            //     anoArray(ano);
            //     etiqueta = `${etiquetaCambiad}`
            //     break;
            default:
                break;
        }
    }
    switch (construye) {
        case 1:
            mesArray(mes);
            etiqueta = mesesNombre[mes]
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
                    <div on:click={()=>{celdaSeleccionada(data.imprimir,construye)}} class="{data.style}">{data.dia}</div>
                    <!-- <div class="{data.style}">{data.dia}</div> -->
                {/each}
            </div>
        {/if}
        {#if construye === 2}
            <div class="gridMesesAno col-sm-12" id="calenMeses">
                {#each infoImprimir as data,i }
                    <div on:click={()=>{celdaSeleccionada(data.dia,construye)}}  class="{data.style}"><p>{data.imprimir}</p></div>
                {/each}
            </div>
        {/if}
        {#if construye === 3}
            <div class="gridMesesAno col-sm-12" id="calenAno">
                {#each infoImprimir as data,i }
                    <div on:click={()=>{celdaSeleccionada(data.dia,construye)}} class="{data.style}"><p>{data.imprimir}</p></div>
                {/each}
            </div>
        {/if}
    </div>
</div>