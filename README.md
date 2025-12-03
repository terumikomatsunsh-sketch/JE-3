[quiz_part2.html](https://github.com/user-attachments/files/23896806/quiz_part2.html)
<!doctype html>
<html lang="ja">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>英語クイズ（第2部）</title>
<style>
body{font-family:-apple-system,Meiryo;padding:18px;background:#f7f9f9}
.card{background:#fff;padding:16px;margin-bottom:14px;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.06)}
.question{font-weight:600;margin-bottom:8px}
.choice{display:flex;gap:8px;padding:8px;border:1px solid #ddd;border-radius:8px;margin-bottom:6px;cursor:pointer;}
.choice:hover{background:#f0f0f0;}
.result{margin-top:8px;padding:8px;border-radius:8px;font-weight:600;display:none}
.correct{background:#ecffef;border:1px solid #9ef0b8}
.wrong{background:#ffecec;border:1px solid #ffb3b3}
.explain{margin-top:6px;font-weight:normal;}
</style>
</head>
<body>
<h1>英語クイズ（第2部）</h1>

<p style="margin-top: 20px;">
  <a href="index.html" download="英語クイズ（第2部）.html" style="padding: 10px 15px; background-color: #007bff; color: white; text-decoration: none; border-radius: 5px;">
    このクイズをダウンロードして保存する
  </a>
</p>

<div id="quiz"></div>
<script>
const data = [
 {id:18,q:"Ms. Smith is my homeroom teacher. She has three years of (    ) as a teacher.",choices:["a. information","b. experience","c. housework","d. engineer"],answer:"b",explain:"「experience (経験)」が「3 years of experience (3年間の経験)」として先生のキャリアを表すのに適切です。"},
 {id:19,q:"A: Do you (    ) our trip to Tokyo ten years ago? B: Yes, I really enjoyed the bus tour.",choices:["a. remember","b. feel","c. enter","d. notice"],answer:"a",explain:"「remember (覚えている)」は、過去の出来事や思い出について尋ねるときに使います。"},
 {id:20,q:"My sister's hairstyle is (    ) mine. She has short hair, but I have long hair.",choices:["a. late for","b. afraid of","c. different from","d. full of"],answer:"c",explain:"「different from (〜と違っている)」は、お姉さんと自分の髪型が違うことを説明するのに正しい表現です。"}
];

function createQuestion(item){
  let w=document.createElement("div");w.className="card";
  let q=document.createElement("div");q.className="question";q.textContent=`(${item.id}) `+item.q;w.appendChild(q);

  item.choices.forEach((t,i)=>{
    const choiceValue = String.fromCharCode(97 + i); // a, b, c, d
    let lab=document.createElement("label");
    lab.className="choice";
    
    let r=document.createElement("input");
    r.type="radio";
    r.name="q"+item.id;
    r.value=choiceValue;
    r.style.display = "none"; // ラジオボタン本体は非表示
    
    // ラベル全体をクリックで解答できるように設定
    lab.onclick=()=>show(item, choiceValue, w);

    lab.appendChild(document.createTextNode(t)); // テキストのみ表示
    w.appendChild(lab);
  });
  
  let res=document.createElement("div");res.className="result";w.appendChild(res);
  return w;
}

function show(item, val, wrap){
  // 既に解答済みなら何もしない
  if (wrap.dataset.answered) return;

  let res=wrap.querySelector(".result");
  res.style.display="block";

  // 全ての選択肢のクリックイベントを無効化
  wrap.querySelectorAll('.choice').forEach(choice => {
    choice.onclick = null;
    choice.style.cursor = 'default';
  });
  wrap.dataset.answered = 'true'; // 解答済みマーク

  if(val===item.answer){
    res.className="result correct";
    res.innerHTML="**正解！**<div class='explain'>【中学1年生向け解説】 "+item.explain+"</div>";
  }else{
    const idx=item.answer.charCodeAt(0)-97;
    const correct=item.choices[idx];
    res.className="result wrong";
    res.innerHTML="**不正解。**正しい答えは "+correct+" です。<div class='explain'>【中学1年生向け解説】 "+item.explain+"</div>";
  }
}

// ページ読み込み時にクイズを作成
document.addEventListener('DOMContentLoaded', () => {
    data.forEach(x => document.getElementById("quiz").appendChild(createQuestion(x)));
});
</script>
</body>
</html>
