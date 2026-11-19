# chia-bill
Share bill
[Uploading index.html…]()
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#e6f7ec">
<title>Chia tiền đi ăn 🍲</title>
<style>
:root{
  --bg:#e6f7ec; --card:#ffffff; --ink:#0f2a1a; --muted:#4d6b5a;
  --green:#00b14f; --green-dark:#008a3d; --green-soft:#c9efd7; --line:#b9e3c9;
}
@media (prefers-color-scheme: dark){
  :root{ --bg:#0e2217; --card:#16301f; --ink:#eafaf0; --muted:#9cc4ab;
    --green:#2fd36f; --green-dark:#1fae58; --green-soft:#1f4a2f; --line:#2a5a3b; }
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0}
body{
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  background:var(--bg); color:var(--ink); font-size:18px; line-height:1.4;
  padding:max(16px,env(safe-area-inset-top)) 16px max(24px,env(safe-area-inset-bottom));
}
main{max-width:480px;margin:0 auto;display:flex;flex-direction:column;gap:14px}
h1{font-size:26px;margin:4px 0 0;font-weight:800}
.sub{margin:0;color:var(--muted);font-size:16px}
.card{background:var(--card);border-radius:24px;padding:18px;box-shadow:0 2px 0 var(--line)}
label,.lbl{display:block;font-size:17px;font-weight:700;color:var(--muted);margin-bottom:8px}
.money{display:flex;align-items:baseline;gap:8px;border-bottom:3px solid var(--green);padding-bottom:6px}
.money input{
  flex:1;min-width:0;border:0;background:transparent;color:var(--ink);outline:none;
  font-family:inherit;font-weight:800;font-size:44px;line-height:1.1;padding:0;
}
.money input::placeholder{color:var(--green-soft)}
.money span{font-size:28px;font-weight:800;color:var(--green)}
.chips{display:flex;gap:8px;margin-top:12px;flex-wrap:wrap}
.chip{
  border:0;background:var(--green-soft);color:var(--green-dark);font-family:inherit;font-weight:700;font-size:17px;line-height:1.2;
  padding:10px 16px;border-radius:999px;cursor:pointer;min-height:44px;
}
@media (prefers-color-scheme: dark){.chip{color:var(--green)}}
.chip:active{transform:scale(.96)}
.people{display:flex;align-items:center;justify-content:space-between}
.people .n{font-size:52px;font-weight:800;min-width:90px;text-align:center}
.round{
  width:68px;height:68px;border-radius:50%;border:0;background:var(--green);color:#fff;
  font-family:inherit;font-weight:700;font-size:40px;line-height:1;cursor:pointer;
}
.round:active{transform:scale(.92);background:var(--green-dark)}
.round:disabled{background:var(--green-soft);color:var(--muted);cursor:not-allowed}
.opt{display:flex;align-items:center;justify-content:space-between;gap:12px;padding:10px 0;font-size:18px;font-weight:600}
.opt + .opt{border-top:1px solid var(--line)}
.opt input{width:28px;height:28px;accent-color:var(--green);flex:none}
.opt small{display:block;color:var(--muted);font-weight:500;font-size:15px}
.result{background:var(--green);color:#fff;border-radius:28px;padding:22px 18px;text-align:center}
.result .t{font-size:18px;font-weight:600;opacity:.95}
.result .big{font-size:58px;font-weight:800;line-height:1.1;margin:6px 0 2px;word-break:break-word}
.result .per{font-size:18px;font-weight:600;opacity:.95}
.break{display:grid;grid-template-columns:1fr auto;gap:6px 12px;font-size:17px}
.break dt{color:var(--muted)} .break dd{margin:0;font-weight:700;text-align:right}
.break .sum{border-top:2px solid var(--line);padding-top:8px;margin-top:2px;color:var(--ink);font-weight:800}
.copy{
  width:100%;border:0;border-radius:20px;background:var(--ink);color:var(--bg);
  font-family:inherit;font-weight:800;font-size:20px;line-height:1.2;padding:18px;min-height:60px;cursor:pointer;
}
.copy:active{transform:scale(.98)}
.copy:disabled{opacity:.35;cursor:not-allowed}
.hint{color:var(--muted);font-size:15px;text-align:center;margin:0}
.toast{
  position:fixed;left:50%;bottom:max(24px,env(safe-area-inset-bottom));transform:translate(-50%,20px);
  background:var(--ink);color:var(--bg);padding:14px 22px;border-radius:999px;font-weight:700;
  opacity:0;pointer-events:none;transition:.2s;
}
.toast.show{opacity:1;transform:translate(-50%,0)}
:focus-visible{outline:3px solid var(--green-dark);outline-offset:2px}
@media (prefers-reduced-motion: reduce){*{transition:none!important}}
</style>
</head>
<body>
<main>
  <header>
    <h1>Chia tiền ăn chung 🍲</h1>
    <p class="sub">Nhập bill, chọn số người, xong!</p>
  </header>

  <section class="card">
    <label for="bill">💰 Tổng bill</label>
    <div class="money">
      <input id="bill" type="text" inputmode="numeric" autocomplete="off" placeholder="850,000" aria-label="Tổng bill bằng đồng">
      <span>đ</span>
    </div>
    <div class="chips" aria-label="Cộng nhanh">
      <button class="chip" data-add="50000">+50k</button>
      <button class="chip" data-add="100000">+100k</button>
      <button class="chip" data-add="500000">+500k</button>
      <button class="chip" id="clear">Xóa</button>
    </div>
  </section>

  <section class="card">
    <div class="lbl">👫 Số người</div>
    <div class="people">
      <button class="round" id="minus" aria-label="Giảm một người">−</button>
      <div class="n" id="count" aria-live="polite">4</div>
      <button class="round" id="plus" aria-label="Thêm một người">+</button>
    </div>
  </section>

  <section class="card">
    <div class="opt">
      <div>🧾 VAT 10%<small>Thuế giá trị gia tăng</small></div>
      <input type="checkbox" id="vat" checked aria-label="Tính VAT 10%">
    </div>
    <div class="opt">
      <div>🙏 Tip 5%<small>Cho nhân viên phục vụ</small></div>
      <input type="checkbox" id="tip" checked aria-label="Tính tip 5%">
    </div>
  </section>

  <section class="result" aria-live="polite">
    <div class="t">Mỗi người trả</div>
    <div class="big" id="each">0đ</div>
    <div class="per" id="people-note">cho 4 người</div>
  </section>

  <section class="card">
    <dl class="break">
      <dt>Bill gốc</dt><dd id="r-bill">0đ</dd>
      <dt>VAT 10%</dt><dd id="r-vat">0đ</dd>
      <dt>Tip 5%</dt><dd id="r-tip">0đ</dd>
      <dt class="sum">Tổng cộng</dt><dd class="sum" id="r-total">0đ</dd>
    </dl>
  </section>

  <button class="copy" id="copy" disabled>📋 Copy kết quả</button>
  <p class="hint">Làm tròn đến nghìn đồng. Không lưu dữ liệu nào cả.</p>
</main>
<div class="toast" id="toast" role="status">Đã copy! ✅</div>

<script>
(function(){
  var MIN = 1, MAX = 50;
  var bill = 0, people = 4;
  var $ = function(id){ return document.getElementById(id); };
  var fmt = function(n){ return Math.round(n).toLocaleString("en-US") + "đ"; };

  var billEl = $("bill");

  function setBill(n){
    bill = Math.max(0, Math.min(n, 999999999));
    billEl.value = bill ? bill.toLocaleString("en-US") : "";
    render();
  }

  billEl.addEventListener("input", function(){
    var digits = billEl.value.replace(/\D/g, "");
    setBill(digits ? parseInt(digits, 10) : 0);
  });

  document.querySelectorAll("[data-add]").forEach(function(b){
    b.addEventListener("click", function(){ setBill(bill + parseInt(b.dataset.add, 10)); });
  });
  $("clear").addEventListener("click", function(){ setBill(0); billEl.focus(); });

  $("minus").addEventListener("click", function(){ if (people > MIN){ people--; render(); } });
  $("plus").addEventListener("click", function(){ if (people < MAX){ people++; render(); } });
  $("vat").addEventListener("change", render);
  $("tip").addEventListener("change", render);

  var last = { text: "" };

  function render(){
    var vat = $("vat").checked ? bill * 0.10 : 0;
    var tip = $("tip").checked ? bill * 0.05 : 0;
    var total = bill + vat + tip;
    var each = Math.round(total / people / 1000) * 1000;

    $("count").textContent = people;
    $("minus").disabled = people <= MIN;
    $("plus").disabled = people >= MAX;
    $("each").textContent = fmt(each);
    $("people-note").textContent = "cho " + people + " người";
    $("r-bill").textContent = fmt(bill);
    $("r-vat").textContent = fmt(vat);
    $("r-tip").textContent = fmt(tip);
    $("r-total").textContent = fmt(total);
    $("copy").disabled = bill <= 0;

    var extras = [];
    if ($("vat").checked) extras.push("VAT 10%");
    if ($("tip").checked) extras.push("tip 5%");
    last.text = "🍲 Chia tiền ăn chung\n" +
      "Bill: " + fmt(bill) + (extras.length ? " (+ " + extras.join(" + ") + ")" : "") + "\n" +
      "Tổng cộng: " + fmt(total) + "\n" +
      "👉 Mỗi người trả: " + fmt(each) + " (" + people + " người)";
  }

  var toastEl = $("toast"), timer;
  function toast(msg){
    toastEl.textContent = msg;
    toastEl.classList.add("show");
    clearTimeout(timer);
    timer = setTimeout(function(){ toastEl.classList.remove("show"); }, 1800);
  }

  function fallbackCopy(text){
    var ta = document.createElement("textarea");
    ta.value = text; ta.style.position = "fixed"; ta.style.opacity = "0";
    document.body.appendChild(ta); ta.select();
    var ok = false;
    try { ok = document.execCommand("copy"); } catch(e){}
    document.body.removeChild(ta);
    return ok;
  }

  $("copy").addEventListener("click", function(){
    var text = last.text;
    if (navigator.clipboard && window.isSecureContext){
      navigator.clipboard.writeText(text).then(
        function(){ toast("Đã copy! ✅"); },
        function(){ toast(fallbackCopy(text) ? "Đã copy! ✅" : "Không copy được 😢"); }
      );
    } else {
      toast(fallbackCopy(text) ? "Đã copy! ✅" : "Không copy được 😢");
    }
  });

  render();
})();
</script>
</body>
</html>
