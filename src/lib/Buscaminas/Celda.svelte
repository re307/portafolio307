<script>
    export let data;
    let vecinas;
    let liberada = false;
    let cercania = 0;
    if (data.isBorde) {
        if (data.izquierdo) {
            if (data.superior) {
                vecinas = [(data.numero+1),(data.numero+(data.largo+1)),data.numero+data.largo];
            }else
                if (data.inferior) {
                    vecinas = [(data.numero+1),(data.numero-data.largo),(data.numero-(data.largo+1))];
                }else{
                    vecinas = [(data.numero+1),(data.numero+(data.largo+1)),data.numero+data.largo,(data.numero-data.largo),((data.numero-data.largo)+1)];
                }
            
        }else
            if (data.derecho) {
                if (data.superior) {
                    vecinas = [(data.numero+data.largo),((data.numero+data.largo)-1),(data.numero-1)]
                }else
                    if (data.inferior) {
                        vecinas = [(data.numero-1),((data.numero-data.largo)-1),(data.numero-data.largo)]
                    }else{
                        vecinas = [(data.numero+data.largo),((data.numero+data.largo)-1),(data.numero-1),((data.numero-data.largo)-1),(data.numero-data.largo)]
                    }
                
            }
    }else{
        if (data.superior) {
                vecinas = [(data.numero+1),((data.numero+data.largo)+1),(data.numero+data.largo),((data.numero+data.largo)-1),(data.numero-1)]
        }else
            if (data.inferior) {
                vecinas = [(data.numero+1),(data.numero-1),((data.numero-data.largo)-1),(data.numero-data.largo),((data.numero-data.largo)+1)]
            }else{
                vecinas = [(data.numero+1),((data.numero+data.largo)+1),(data.numero+data.largo),((data.numero+data.largo)-1),(data.numero-1),((data.numero-data.largo)-1),(data.numero-data.largo),((data.numero-data.largo)+1)]
            }
    }
    if (data.isBomba) {
        vecinas.forEach((vecina)=>{
            setTimeout(()=>{
                let celdaCercania = document.getElementById(`cercania${vecina}`);
                let cercania = celdaCercania.innerText;
                let cantidad = Number(cercania);
                celdaCercania.innerText = `${cantidad++}`;
            },1000);
        });
    }
    let destapaVecinas = ()=>{
        if (!liberada) {
            let celda = document.getElementById(`celda${data.numero}`);
            celda.className = "celda_libre";
            // celda.childNodes[0].style.display = "block";
            liberada = true;
            vecinas.forEach(element => {
                // console.log(element)
                setTimeout(()=>{
                    document.getElementById(`celda${element}`).click();
                },1);
            });
        }
    }
    let determinaColor = ()=>{
        let color = "";
        switch (cercania) {
            case 0:
                color = "black";
                break;
            case 1:
                color = "blue";
                break;
            default:
                break;
        }
    }
</script>
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="celda" id="celda{data.numero}"
    on:click={destapaVecinas}
>
    <div style="display: {liberada?'block':'none'};">
        {#if data.isBomba}
            <img class="logo" alt="Vite logo" />
        {:else}
            <p id="cercania{data.numero}">{cercania}</p>
        {/if}
    </div>
</div>