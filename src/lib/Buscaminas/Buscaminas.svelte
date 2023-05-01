<script>
    import './buscaminas.css'
    import Celda from './Celda.svelte'
    let largo = 18;
    let totalCeldas = largo * 18;
    let filas = new Array(totalCeldas);
    let celdasBombas = new Array();

    let totalBombas = Math.round(totalCeldas / 8);
    for (let index = 1; index <= totalBombas; index++) {
        let celdaBomba = Math.floor(Math.random() * totalCeldas) + 1;
        celdasBombas.push(celdaBomba);
    }
    let isBorde = (celda) =>{
        let result = false;
        if (celda%largo<2) {
            result = true;
        }
        return result;
    }
    let isBordeIzquierdo = (celda) =>{
        let result = false;
        if (celda%largo == 1) {
            result = true;
        }
        return result;
    }
    let isBordeDerecho = (celda) =>{
        let result = false;
        if (celda%largo == 0) {
            result = true;
        }
        return result;
    }
    let isBordeSuperior = (celda)=>{
        let result = false;
        if ((celda-largo)<1) {
            result = true;
        }
        return result
    }
    let isBordeInferior = (celda)=>{
        let result = false;
        if ((largo+celda)>totalCeldas) {
            result = true;
        }
        return result
    }
</script>
<div class="container juego_b">
    <div class="row marcador">
        macador
    </div>
    <div id="tablero" class="row tablero">
        {#each filas as fila,i }
            <Celda data={{
                "numero":i+1,
                "largo":largo,
                "ancho":totalCeldas,
                "isBorde":isBorde(i+1),
                "izquierdo":isBordeIzquierdo(i+1),
                "derecho":isBordeDerecho(i+1),
                "superior":isBordeSuperior(i+1),
                "inferior":isBordeInferior(i+1),
                "isBomba":celdasBombas.includes(i+1)
            }}>
            </Celda>
        {/each}
    </div>
</div>