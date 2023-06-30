<script>
    import './lineaTiempo.css'
    let lineatiempo = [
        {
            "idEstatus":"Finalizado"
            ,"Fecha":"30/06/2023 13:30"
        },
        {
            "idEstatus":"Aprovado"
            ,"Fecha":"29/06/2023 13:30"
        },
        {
            "idEstatus":"Asignado"
            ,"Fecha":"28/06/2023 13:30"
        }
    ];
    let continerBoxs = '';
    lineatiempo.forEach((value) => {
        console.log(value);
        continerBoxs += `
            <div class="box">
                <p>
                    ${value.idEstatus}
                    <br>
                    ${value.Fecha}
                </p>
            </div>
        `;
    });
</script>
<div class="container">
    {@html continerBoxs}
</div>