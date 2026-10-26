# student-grade-calculator
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Student Grade Calculator</title>
<style>
body{margin:0;padding:25px;background:#111827;color:#f9fafb;font-family:Arial}
main{max-width:500px;margin:auto;background:#1f2937;padding:25px;border-radius:16px}
input{width:100%;box-sizing:border-box;padding:12px;margin:8px 0 14px;border:1px solid #475569;border-radius:8px;background:#111827;color:white}
button{padding:12px 18px;background:#38bdf8;border:0;border-radius:8px;cursor:pointer;font-weight:bold}
.result{margin-top:20px;padding:18px;background:#293548;border-radius:10px;line-height:1.8}
</style>
</head>
<body>
<main>
<h1>🎓 Grade Calculator</h1>
<p>Enter marks for five subjects out of 100.</p>
<form id="form">
<div id="subjects"></div>
<button>Calculate Result</button>
</form>
<div class="result" id="result" aria-live="polite">Your result will appear here.</div>
</main>
<script>
const subjects=document.getElementById("subjects");
["English","Mathematics","Subject 3","Subject 4","Subject 5"].forEach((s,i)=>{
const label=document.createElement("label");
label.textContent=s+" marks";
label.htmlFor="mark"+i;
const input=document.createElement("input");
input.id="mark"+i;
input.type="number";
input.min="0";
input.max="100";
input.step="0.01";
input.required=true;
input.placeholder="0–100";
subjects.append(label,input);
});
document.getElementById("form").onsubmit=e=>{
e.preventDefault();
const marks=[0,1,2,3,4].map(i=>Number(document.getElementById("mark"+i).value));
const out=document.getElementById("result");
if(marks.some((m,i)=>document.getElementById("mark"+i).value===""||m<0||m>100)){
out.textContent="Each subject must have marks between 0 and 100.";return;
}
const total=marks.reduce((a,b)=>a+b,0);
const avg=total/marks.length;
const grade=avg>=90?"A+":avg>=80?"A":avg>=70?"B":avg>=60?"C":avg>=50?"D":avg>=40?"E":"F";
out.innerHTML=`Total: ${total} / 500<br>Percentage: ${avg.toFixed(2)}%<br>Grade: ${grade}<br>Result: ${marks.some(m=>m<33)?"Review subjects below 33 marks":"Calculated successfully"}`;
};
</script>
</body>
</html>
