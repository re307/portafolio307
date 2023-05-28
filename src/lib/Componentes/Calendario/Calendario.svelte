<script>
    import './calendario.css'
    const fechaActual = new Date();
    let htmlInicial = ``;
    let mesInicial = fechaActual.getMonth()+1;
    let mes = fechaActual.getMonth()+1;
    let ano = fechaActual.getFullYear();

    let todoCalendario = ()=>{
        let díaUnoAnual = new Date(`${fechaActual.getUTCFullYear()}-01-01 00:00:00`);
        let nuevoGrid = '';
        let actDesAct = 'mesDesActivo';
        let styledes ='style="width: 5px;height: 5px;"';
        for (let ai = 1; ai < 12; ai++) {
            let diainicio = new Date(`${fechaActual.getUTCFullYear()}-${ai}-01 00:00:00`);
            if (ai>1) {
                diainicio.setDate(diainicio.getDate()-diainicio.getDay());
            }
            nuevoGrid = nuevoGrid+`
                <div class="col-sm-1 gridDSMA ${actDesAct}"${styledes}>
            <div class="dia">do.</div>
            <div class="dia">lu.</div>
            <div class="dia">ma.</div>
            <div class="dia">mi.</div>
            <div class="dia">ju.</div>
            <div class="dia">vi.</div>
            <div class="dia">sa.</div>
            `;
            for (let index = 1; index < 43; index++) {
                nuevoGrid =nuevoGrid+`
                    <div class="${diainicio.toDateString()==fechaActual.toDateString()?'actual':'celda'}">${diainicio.getDate()}</div>
                `;
                diainicio.setDate(diainicio.getDate()+1);
            }
            nuevoGrid = nuevoGrid+`</div>`;
            if (diainicio.getMonth()==fechaActual.getMonth()) {
                actDesAct = 'mesActivo';
                styledes='';
            }else{actDesAct = 'mesDesActivo';styledes ='style="width: 5px;height: 5px;"';}
            
        }
        // console.log('nuevoGrid: ',nuevoGrid);
        htmlInicial = nuevoGrid;
    }
    let mesVista = (mesVisual)=>{
        console.log('mesVisual: ',mesVisual);
        htmlInicial ='';
        let mesPintar ;
        let mesNumero = mesVisual;
        if (mesNumero == 13) {
            mesNumero = 1;
            mesInicial = 1;
            ano = ano + 1 ;
        }
        if (mesNumero == 0) {
            mesNumero = 12;
            mesInicial = 12;
            ano=ano-1;
        }
        mesPintar = new Date(`${ano}-${mesNumero}-01 00:00:00`);
        console.log(`${ano}-${mesNumero}-01 00:00:00`);
        mesPintar.setDate(mesPintar.getDate()-mesPintar.getDay());
        console.log(mesPintar.toString());
        let mesGrid = `
                <div class="gridDSMA col-sm-12">
            <div class="dia">do.</div>
            <div class="dia">lu.</div>
            <div class="dia">ma.</div>
            <div class="dia">mi.</div>
            <div class="dia">ju.</div>
            <div class="dia">vi.</div>
            <div class="dia">sa.</div>
            `;
        for (let index = 1; index < 43; index++) {
            mesGrid =mesGrid+`
                <div class="${mesPintar.toDateString()==fechaActual.toDateString()?'actual':'celda'}">${mesPintar.getDate()}</div>
            `;
            mesPintar.setDate(mesPintar.getDate()+1);
        }
        mesGrid = mesGrid+`</div>`;
        htmlInicial = mesGrid;
    }
    mesVista(mes);
</script>
<div class="container sinpadding">
    <div class="row">
        <div class="col-sm-4 previo btn-cand" on:click={()=>{mesInicial=mesInicial-1;mesVista(mesInicial)}}>Previo</div>
        <div class="col-sm-4 muestraInfoDe">{@html mesInicial}</div>
        <div class="col-sm-4 siguiente btn-cand" on:click={()=>{mesInicial=mesInicial+1;mesVista(mesInicial)}}>Siguiente</div>
    </div>
    <div class="row">
        {@html htmlInicial}
    </div>
</div>