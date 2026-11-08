# Italy Net Pay Calculator

> From gross to net in Italy in 2026: employee social security, income tax (IRPEF) with employment credits, regional and municipal surcharges, for Milan, Rome, Turin, Bologna and Naples.


<section> <span class="eyebrow">Net pay calculator</span> <h1 id="what-your-employee-takes-home-in-italy">What your employee takes home in Italy</h1> <p class="lede">Enter the annual gross salary and the city. The estimate applies 2026 rules: employee social security, income tax with employment credits and the local surcharges.</p> </section> <section> <div class="grid"> <form class="panel" id="nf" style="display:grid;gap:16px"> <label for="g">Annual gross salary, RAL (EUR)<input id="g" type="number" min="10000" step="1000" value="50000"></label> <label for="city">City<select id="city"><option>Milan</option><option>Rome</option><option>Turin</option><option>Bologna</option><option>Naples</option></select></label> <label for="inst">Paid in<select id="inst"><option value="13">13 installments</option><option value="14">14 installments</option><option value="12">12 (13th/14th pro-rata)</option></select></label> </form> <div class="panel" style="min-width:0"><div class="tbl"><table id="nt"><thead><tr><th>Item</th><th class="num">Per year</th></tr></thead><tbody></tbody></table></div> <p id="nm" style="margin-bottom:0;font-weight:600"></p></div> </div>  </section> <section class="prose"> <h2 id="how-the-calculation-works">How the calculation works</h2> <ol> <li>The employee pays 9.19% social security on gross pay, plus 1% on the part above €56,224 a year.</li> <li>Income tax (IRPEF) applies to what remains: 23% up to €28,000, 33% from €28,000 to €50,000, 43% above.</li> <li>Employment tax credits reduce the tax. They are largest on low salaries and reach zero at €50,000. Between €20,000 and €40,000 an extra credit of up to €1,000 applies.</li> <li>The regional and municipal surcharges are added, unless income is below the city's exemption threshold.</li> </ol> <p>None of this changes what you pay as employer: see the <a href="calculator.html">employer cost calculator</a>.</p> </section> <script>(function(){const N = {"status":"secondary","source":"data/params/2026.yaml (irpef, inps, addizionali); TUIR art. 11 and 13; L. 207/2024; L. 199/2025","employee_inps":0.0919,"extra_1pct_above":56224,"irpef":[[28000,0.23],[50000,0.33],[null,0.43]],"cities":{"Milan":{"region":"Lombardy","regional":[[null,0.0123]],"municipal":0.008,"exempt":23000},"Rome":{"region":"Lazio","regional":[[28000,0.0173],[null,0.0333]],"municipal":0.009,"exempt":14000},"Turin":{"region":"Piedmont","regional":[[null,0.0162]],"municipal":0.008,"municipal_note":"0.8% to 1.2% by band; 0.8% used","exempt":11790},"Bologna":{"region":"Emilia-Romagna","regional":[[null,0.0133]],"municipal":0.008,"exempt":15000},"Naples":{"region":"Campania","regional":[[null,0.0173]],"municipal":0.01,"exempt":12000}}};

const eur = n => (n < 0 ? '−€' : '€') + Math.round(Math.abs(n)).toLocaleString('en-US');
function bands(x, b){ let t = 0, lo = 0; for (const [hi, r] of b){ const top = hi ?? Infinity; if (x > lo) t += (Math.min(x, top) - lo) * r; lo = top; } return t; }
function credit(r){ if (r <= 15000) return 1955; if (r <= 28000) return 1910 + 1190 * (28000 - r) / 13000; if (r <= 50000) return 1910 * (50000 - r) / 22000 + (r > 25000 && r <= 35000 ? 65 : 0); return 0; }
function extra(r){ if (r > 20000 && r <= 32000) return 1000; if (r > 32000 && r < 40000) return 1000 * (40000 - r) / 8000; return 0; }
function calc(){
  const g = +document.getElementById('g').value || 0, c = N.cities[document.getElementById('city').value], n = +document.getElementById('inst').value;
  const inps = g * N.employee_inps + Math.max(0, g - N.extra_1pct_above) * 0.01;
  const tx = g - inps;
  const irpef = Math.max(0, bands(tx, N.irpef) - credit(tx) - extra(tx));
  const reg = bands(tx, c.regional), mun = tx > c.exempt ? tx * c.municipal : 0;
  const net = g - inps - irpef - reg - mun;
  const rows = [['Gross salary', g], ['Employee social security', -inps], ['Income tax (IRPEF) after credits', -irpef], [`Regional surcharge (${c.region})`, -reg], ['Municipal surcharge', -mun]];
  document.querySelector('#nt tbody').innerHTML = rows.map(([k, v]) => `<tr><td>${k}</td><td class="num">${eur(v)}</td></tr>`).join('') + `<tr><td><b>Net pay</b></td><td class="num"><b>${eur(net)}</b></td></tr>`;
  document.getElementById('nm').textContent = `About ${eur(net / n)} net in each of ${n} monthly payslips (${(net / g * 100).toFixed(0)}% of gross).`;
}
document.getElementById('nf').addEventListener('input', calc); document.getElementById('nf').addEventListener('submit', e => e.preventDefault()); calc();
})();</script>


---
Source: https://hiringitaly.com/net-pay-calculator.html
