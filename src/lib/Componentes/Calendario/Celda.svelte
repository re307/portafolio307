<script>

    export let info;
    export let selecionaCalenHijo;
    export let calendario = info.seleccionado;
    

    const hoy = new Date();
    const mesActual = hoy.getMonth();
    const ano = hoy.getFullYear();
    const mesesNombre = ["ENE","FEB","MAR","ABR","MAY","JUN","JUL","AGO","SEP","OCT","NOV","DIC"];
    let fechaIngresada = new Date(info.imprime);
    console.log('fechaIngresada: ',fechaIngresada.toString());
    let styleS = null;
    let htmlInsert = null;
    switch (info.seleccionado) {
        case 1:
            if (fechaIngresada.toDateString() === hoy.toDateString()) {
                styleS = "dia_actual";
            }else{
                styleS = "dia_libre";
            }
            htmlInsert = fechaIngresada.getDate()
            break;
        case 2:
            if (mesActual === info.imprime.mes&&ano ===info.imprime.ano) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            htmlInsert = `<p>${mesesNombre[info.imprime.mes]}</p>`
            break;
        case 3:
            if (ano ===info.imprime) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            htmlInsert = `<p>${info.imprime}</p>`
            break;
    
        default:
            break;
    }
    let validaEcucion = ()=>{
        if (info.seleccionado > 1) {
            calendario = info.seleccionado-1;
        }
    }
</script>
<div on:click={()=>{validaEcucion(),selecionaCalenHijo()}} class="{styleS}">{@html htmlInsert}</div>
