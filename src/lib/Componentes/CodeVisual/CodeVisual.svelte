<script>
    import './codeVsiaul.css'
    import ejemplo from '../../../assets/ejemplo.json';
    let linea = 0;
    const evaluaObjeto = (evaluar,lineaExterna = 0)=>{
        var type = Object.prototype.toString.call(evaluar);
        var htmlSalida = "";
        switch(type){
            case '[object Array]':
                linea = 1+linea;
                htmlSalida =`
                    <div class="token-line _34NUj">
                        <div aria-hidden="true" class="_1UDBA">${linea}</div>
                        <div class="_3GF8E">
                            <span class="token punctuation">[</span>
                            <span class="token plain"></span>
                        </div>
                    </div>`;
                evaluar.forEach(element => {
                    htmlSalida +=evaluaObjeto(element,linea);
                });
                linea = 1+linea;
                htmlSalida +=`
                    <div class="token-line _34NUj">
                        <div aria-hidden="true" class="_1UDBA">${linea}</div>
                        <div class="_3GF8E">
                            <span class="token punctuation">]</span>
                            <span class="token plain"></span>
                        </div>
                    </div>`;
                return htmlSalida;
            break;

            case '[object Object]':
                linea = linea+1;
                htmlSalida = `
                    <div class="token-line _34NUj">
                        <div aria-hidden="true" class="_1UDBA">${linea}</div>
                        <div class="_3GF8E">
                            <span class="_3tPKe">
                                <span class="_1U1x7">
                                    <span class="_1piIL">  </span>
                                    <span class="_19kcq">
                                        <span class="token plain"></span>
                                        <span class="token punctuation">{</span>
                                        <span class="token plain"></span>
                                    </span>
                                </span>
                            </span>
                        </div>`;
                for(var info in evaluar){
                    linea = linea+1;
                    htmlSalida += `
                        <div class="token-line _34NUj">
                            <div aria-hidden="true" class="_1UDBA">${linea}</div>
                            <div class="_3GF8E">
                                <span class="_3tPKe">
                                    <span class="_1U1x7">
                                        <span class="_1piIL">    </span>
                                        <span class="_19kcq">
                                            <span class="token plain"></span>
                                            <span class="token string-property property">"${info}"</span>
                                            <span class="token operator">:</span>
                                            <span class="token plain"> </span>
                                            ${evaluaObjeto(evaluar[info],linea)}
                                            <span class="token punctuation">,</span>
                                            <span class="token plain"></span>
                                        </span>
                                    </span>
                                </span>
                            </div>
                        </div>`;
                }
                linea = linea+1;
                htmlSalida +=`
                        <div class="token-line _34NUj">
                            <div aria-hidden="true" class="_1UDBA">${linea}</div>
                            <div class="_3GF8E">
                                <span class="_3tPKe">
                                    <span class="_1U1x7">
                                        <span class="_1piIL">  </span>
                                        <span class="_19kcq">
                                            <span class="token plain"></span>
                                            <span class="token punctuation">}</span>
                                            <span class="token punctuation">,</span>
                                            <span class="token plain"></span>
                                        </span>
                                    </span>
                                </span>
                            </div>
                        </div>`;
                return htmlSalida;
            break;

            case '[object String]':
                // x = "string";
                htmlSalida = 
                `<span class="token string">"${evaluar}"</span>`;
                return htmlSalida;
            break;

            case '[object Number]':
                // x = "number";
                htmlSalida = 
                `<span class="token number">${evaluar}</span>`;
                return htmlSalida;
            break;
            case '[object Boolean]':
                htmlSalida = 
                `<span class="token boolena">${evaluar}</span>`;
                return htmlSalida;
            break;
            default:
                console.log(`type: `,type);
            break;
        }
    }
    let htmlCode = `
    <div class="_1iCXf" style="max-height: calc((50 * var(--size-base-lineheight-copy-sm)) + (var(--size-250) * 1.5);">
        <pre class="AGOwr">
            <code class="_121fh _RkyB prism-code language-javascript">`;
                htmlCode += evaluaObjeto(ejemplo);
                
    htmlCode += `           
            </code>
        </pre>
    </div>`;
</script>
{@html htmlCode}
