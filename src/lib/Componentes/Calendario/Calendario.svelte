<script>
    import './calendario.css'
    import Celda from './Celda.svelte'
    const fechaActual = new Date();
    let infoImprimr = new Array();
    let construye = 1;
    let anosSumados = 12;
    const mesesNombre = ["ENE","FEB","MAR","ABR","MAY","JUN","JUL","AGO","SEP","OCT","NOV","DIC"];
    let htmlInicial = ``;
    let etiqueta = '';
    let mesInicial = fechaActual.getMonth()+1;
    let anoInicial = fechaActual.getFullYear();
    let mes = fechaActual.getMonth()+1;
    let ano = fechaActual.getFullYear();
    let mesArray = (mesVisual_A)=>{
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
            infoImprimr.push(mesPintar_A.toString());
            mesPintar_A.setDate(mesPintar_A.getDate()+1);
        }
    }
    let mesesArray = (ano)=>{
        for (let index = 0; index < 12; index++) {
            let infoMes = {
                "ano":ano,
                "mes":index
            }
            infoImprimr.push(infoMes);
        }
    }
    let anoArray = (ano)=>{
        let anoS = `${ano}`;
        let disminucion = Number(anoS[anoS.length-1])+1;
        let inicio = ano - disminucion;
        for (let index = inicio; index < (inicio+anosSumados); index++) {
            infoImprimr.push(index);
        }
    }
    let opcionesGenerar = (construye,mov)=>{
        switch (construye) {
            case 1:
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
                break;
        
            default:
                break;
        }
    }
    let selecionaCalen = ()=>{
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
                etiqueta = `${ano}`
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
            etiqueta = `${ano}`
            break;
    
        default:
            break;
    }
</script>
<div class="container sinpadding">
    <div class="row">
        <div class="col-sm-4 previo btn-cand" on:click={()=>{}}>Previo</div>
        <div class="col-sm-4 muestraInfoDe" on:click={()=>{construye = (construye<4?construye+1:1);selecionaCalen();}}>{@html etiqueta}</div>
        <div class="col-sm-4 siguiente btn-cand" on:click={()=>{}}>Siguiente</div>
    </div>
    <div class="row" id="calendario">
        {#if construye === 1}
            <div class="gridMes col-sm-12">
                <div class="dia">do.</div>
                <div class="dia">lu.</div>
                <div class="dia">ma.</div>
                <div class="dia">mi.</div>
                <div class="dia">ju.</div>
                <div class="dia">vi.</div>
                <div class="dia">sa.</div>
                {#each infoImprimr as data,i }
                    <Celda info={{
                        "seleccionado":construye,
                        "imprime":data
                    }}></Celda>
                {/each}
            </div>
        {/if}
        {#if ((construye === 2)||(construye === 3))}
            <div class="gridMesesAno col-sm-12">
                {#each infoImprimr as data,i }
                    <Celda info={{
                        "seleccionado":construye,
                        "imprime":data
                    }}></Celda>
                {/each}
            </div>
        {/if}
    </div>
</div>