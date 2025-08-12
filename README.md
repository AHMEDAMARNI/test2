<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>إضافة طلب</title>
    <style>
        body {
            font-family: Tahoma, sans-serif;
            background-color: #f8f8f8;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }
        .form-container {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0px 4px 15px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
        }
        h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
        }
        label {
            display: block;
            margin: 10px 0 5px;
            font-weight: bold;
        }
        input, textarea, button {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 14px;
        }
        button {
            background-color: #28a745;
            color: white;
            border: none;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>

<div class="form-container">
    <h2>إضافة طلب جديد</h2>
    <form id="orderForm">
        <input type="hidden" id="sessionId" name="sessionId">

        <label>الاسم الكامل:</label>
        <input type="text" name="name" required>

        <label>رقم الهاتف:</label>
        <input type="tel" name="phone" required>

        <label>الطلب:</label>
        <textarea name="orderDetails" rows="3" required></textarea>

        <label>العنوان:</label>
        <textarea name="address" rows="2" required></textarea>

        <button type="submit">إرسال الطلب</button>
    </form>
</div>

<script>
    // جلب sessionId من الرابط
    const urlParams = new URLSearchParams(window.location.search);
    document.getElementById('sessionId').value = urlParams.get('sessionId');

    document.getElementById('orderForm').addEventListener('submit', async function(e) {
        e.preventDefault();
        
        const formData = new FormData(this);
        const data = {};
        formData.forEach((value, key) => data[key] = value);

        const response = await fetch(['https://YOUR_N8N_WEBHOOK_URL'](https://ahmedalg.app.n8n.cloud/webhook/9f996da2-bc0f-42df-a84f-46630dc123b8), {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify(data)
        });

        if (response.ok) {
            alert('✅ تم إرسال الطلب بنجاح!');
            this.reset();
        } else {
            alert('❌ حدث خطأ أثناء الإرسال.');
        }
    });
</script>

</body>
</html>
