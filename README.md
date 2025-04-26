<!DOCTYPE html><html lang="ur" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>پروگرام مینیو - جی پی ایس نمبر 1 گمبٹ</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Nastaliq Urdu', serif;
            margin: 20px;
            background: linear-gradient(to bottom right, #e0f7fa, #ffffff);
            direction: rtl;
        }
        h1 {
            text-align: center;
            color: #006064;
            margin-bottom: 20px;
            font-size: 32px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
            background: #ffffff;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
        }
        th, td {
            border: 1px solid #b2ebf2;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #4dd0e1;
            color: white;
            font-size: 18px;
        }
        input[type="number"], input[type="text"] {
            width: 90%;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .btn {
            padding: 10px 20px;
            background: #00796b;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 10px;
            margin-top: 10px;
            transition: background 0.3s ease;
        }
        .btn:hover {
            background: #004d40;
        }
        #result, #totalAmount {
            font-size: 20px;
            color: #004d40;
            text-align: center;
            margin-top: 20px;
        }
    </style>
</head>
<body><h1>پروگرام مینیو - جی پی ایس نمبر 1 گمبٹ</h1><table id="expenseTable">
    <thead>
        <tr>
            <th>آئٹم کا نام</th>
            <th>فی کلو/فی یونٹ قیمت</th>
            <th>مقدار</th>
            <th>لاگت</th>
        </tr>
    </thead>
    <tbody>
        <!-- 25 آئٹمز -->
    </tbody>
</table><div>
    <label>مشترکہ فنڈ کی رقم: </label>
    <input type="number" id="sharedFund" value="0">
</div>
<br>
<div>
    <label>کل ساتھیوں کی تعداد: </label>
    <input type="number" id="totalFriends" value="1">
</div>
<br>
<div style="text-align: center;">
    <button class="btn" onclick="calculateTotal()">حساب لگائیں</button>
    <button class="btn" onclick="downloadPDF()">پی ڈی ایف ڈاؤن لوڈ کریں</button>
</div><h2 id="totalAmount"></h2>
<h2 id="result"></h2><script>
let tbody = document.querySelector('#expenseTable tbody');
for (let i = 0; i < 25; i++) {
    let row = document.createElement('tr');
    row.innerHTML = `
        <td><input type="text" placeholder="آئٹم کا نام"></td>
        <td><input type="number" placeholder="قیمت"></td>
        <td><input type="number" placeholder="مقدار"></td>
        <td><span>0</span></td>
    `;
    tbody.appendChild(row);
}

function calculateTotal() {
    let rows = document.querySelectorAll('#expenseTable tbody tr');
    let grandTotal = 0;
    rows.forEach(row => {
        let price = parseFloat(row.children[1].children[0].value) || 0;
        let quantity = parseFloat(row.children[2].children[0].value) || 0;
        let cost = price * quantity;
        row.children[3].children[0].textContent = cost.toFixed(2);
        grandTotal += cost;
    });

    document.getElementById('totalAmount').innerHTML = `کل رقم: ${grandTotal.toFixed(2)} روپے`;

    let sharedFund = parseFloat(document.getElementById('sharedFund').value) || 0;
    let totalFriends = parseInt(document.getElementById('totalFriends').value) || 1;

    let remaining = grandTotal - sharedFund;
    let perFriend = remaining / totalFriends;

    document.getElementById('result').innerHTML = `
        مشترکہ فنڈ: ${sharedFund.toFixed(2)} روپے<br>
        باقی رقم: ${remaining.toFixed(2)} روپے<br>
        فی ساتھی حصہ: ${perFriend.toFixed(2)} روپے
    `;
}

function downloadPDF() {
    window.print();
}
</script></body>
</html>