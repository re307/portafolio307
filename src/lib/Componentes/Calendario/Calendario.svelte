<script>
    import './calendario.css'
    import Celda from './Celda.svelte'
    const fechaActual = new Date();
    let infoImprimr = new Array();
    let construye = 2;
    let htmlInicial = ``;
    let mesInicial = fechaActual.getMonth()+1;
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
        for (let index = inicio; index < (inicio+10); index++) {
            
        }
    }
    if (construye === 1) {
        mesArray(mes);
    }
    if (construye === 2) {
        mesesArray(ano);
    }
</script>
<div class="container sinpadding">
    <div class="row">
        <div class="col-sm-4 previo btn-cand" on:click={()=>{mesInicial=mesInicial-1;mesVista(mesInicial)}}>Previo</div>
        <div class="col-sm-4 muestraInfoDe">{@html mesInicial}</div>
        <div class="col-sm-4 siguiente btn-cand" on:click={()=>{mesInicial=mesInicial+1;mesVista(mesInicial)}}>Siguiente</div>
    </div>
    <div class="row">
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
        {#if construye === 2}
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