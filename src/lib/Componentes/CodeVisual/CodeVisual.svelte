<script>
    import './codeVsiaul.css'
    let htmlCode = `
    <div class="_1iCXf" style="max-height: calc((50 * var(--size-base-lineheight-copy-sm)) + (var(--size-250) * 1.5);">
    <pre class="AGOwr">
        <code class="_121fh _RkyB prism-code language-javascript">
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">1</div>
                <div class="_3GF8E">
                    <span class="token comment">// Session is built by the OAuth process</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">2</div>
                <div class="_3GF8E">
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">3</div>
                <div class="_3GF8E">
                    <span class="token plain"></span>
                    <span class="token keyword keyword-const">const</span>
                    <span class="token plain"> customer </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token keyword keyword-new">new</span>
                    <span class="token plain"> </span>
                    <span class="token class-name">shopify</span>
                    <span class="token class-name punctuation">.</span>
                    <span class="token class-name">rest</span>
                    <span class="token class-name punctuation">.</span>
                    <span class="token class-name">Customer</span>
                    <span class="token punctuation">(</span>
                    <span class="token punctuation">{</span>
                    <span class="token literal-property property">session</span>
                    <span class="token operator">:</span>
                    <span class="token plain"> session</span>
                    <span class="token punctuation">}</span>
                    <span class="token punctuation">)</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">4</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">first_name </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"Steve"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">5</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">last_name </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"Lastnameson"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">6</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">email </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"steve.lastnameson@example.com"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">7</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">phone </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"+15142546011"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">8</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">verified_email </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token boolean">true</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">9</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">addresses </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token punctuation">[</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">10</div>
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
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">11</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"address1"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"123 Oak St"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">12</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"city"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"Ottawa"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">13</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"province"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"ON"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">14</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"phone"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"555-1212"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">15</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"zip"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"123 ABC"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">16</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"last_name"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"Lastnameson"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">17</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"first_name"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"Mother"</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">18</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">    </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token string-property property">"country"</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token string">"CA"</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">19</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">  </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token punctuation">}</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">20</div>
                <div class="_3GF8E">
                    <span class="token plain"></span>
                    <span class="token punctuation">]</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">21</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">password </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"newpass"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">22</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">password_confirmation </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token string">"newpass"</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">23</div>
                <div class="_3GF8E">
                    <span class="token plain">customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token plain">send_email_welcome </span>
                    <span class="token operator">=</span>
                    <span class="token plain"> </span>
                    <span class="token boolean">false</span>
                    <span class="token punctuation">;</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">24</div>
                <div class="_3GF8E">
                    <span class="token plain"></span>
                    <span class="token keyword keyword-await">await</span>
                    <span class="token plain"> customer</span>
                    <span class="token punctuation">.</span>
                    <span class="token function">save</span>
                    <span class="token punctuation">(</span>
                    <span class="token punctuation">{</span>
                    <span class="token plain"></span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">25</div>
                <div class="_3GF8E">
                    <span class="_3tPKe">
                        <span class="_1U1x7">
                            <span class="_1piIL">  </span>
                            <span class="_19kcq">
                                <span class="token plain"></span>
                                <span class="token literal-property property">update</span>
                                <span class="token operator">:</span>
                                <span class="token plain"> </span>
                                <span class="token boolean">true</span>
                                <span class="token punctuation">,</span>
                                <span class="token plain"></span>
                            </span>
                        </span>
                    </span>
                </div>
            </div>
            <div class="token-line _34NUj">
                <div aria-hidden="true" class="_1UDBA">26</div>
                <div class="_3GF8E">
                    <span class="token plain"></span>
                    <span class="token punctuation">}</span>
                    <span class="token punctuation">)</span>
                    <span class="token punctuation">;</span>
                </div>
            </div>
        </code>
    </pre>
</div>`;
</script>
{@html htmlCode}
