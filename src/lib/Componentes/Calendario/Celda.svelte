<script>

    export let info;

    const hoy = new Date();
    const mesActual = hoy.getMonth();
    const ano = hoy.getFullYear();
    const mesesNombre = ["ENE","FEB","MAR","ABR","MAY","JUN","JUL","AGO","SEP","OCT","NOV","DIC"];
    let fechaIngresada = new Date(info.imprime);
    let styleS = null;
    let htmlInsert = null;
    switch (info.seleccionado) {
        case 1:
            if (fechaIngresada.toDateString() === hoy.toDateString()) {
                styleS = "dia_actual";
            }else{
                styleS = "dia_libre";
            }
            htmlInsert = `<div class="${styleS}">${fechaIngresada.getDate()}</div>`
            break;
        case 2:
            if (mesActual === info.imprime.mes&&ano ===info.imprime.ano) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            htmlInsert = `<div class="${styleS}"><p>${mesesNombre[info.imprime.mes]}</p></div>`
            break;
        case 3:
            if (ano ===info.imprime) {
                styleS = "mesAno_actual";
            }else{
                styleS = "mesAno_libre";
            }
            htmlInsert = `<div class="${styleS}"><p>${info.imprime}</p></div>`
            break;
    
        default:
            break;
    }

</script>
{@html htmlInsert}