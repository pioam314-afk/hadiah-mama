[index.html](https://github.com/user-attachments/files/27392368/index.html)
# hadiah-mama<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mom's 50th Golden Voucher Book</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,700&family=Quicksand:wght@400;600&family=Sacramento&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #fdfbf7; /* Off-white/Cream */
            --card-bg: #ffffff;
            --gold-light: #f9e2af;
            --gold-mid: #d4af37; /* Metallic Gold */
            --gold-dark: #aa8a2e;
            --text: #3d3d3d;
        }

        body {
            font-family: 'Quicksand', sans-serif;
            background-color: var(--bg);
            background-image: radial-gradient(#d4af3711 1px, transparent 1px);
            background-size: 20px 20px;
            color: var(--text);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
            border-bottom: 2px solid var(--gold-light);
            padding-bottom: 20px;
        }

        h1 {
            font-family: 'Sacramento', cursive;
            font-size: 4rem;
            background: linear-gradient(to right, var(--gold-dark), var(--gold-mid), var(--gold-dark));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin: 0;
        }

        .sub-header {
            font-family: 'Playfair Display', serif;
            font-style: italic;
            font-size: 1.2rem;
            color: var(--gold-dark);
            margin-top: -10px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            width: 100%;
            max-width: 900px;
        }

        .coupon {
            background: var(--card-bg);
            border: 2px solid var(--gold-mid);
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            position: relative;
            transition: all 0.3s ease;
            box-shadow: 0 10px 20px rgba(212, 175, 55, 0.1);
        }

        .coupon:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(212, 175, 55, 0.2);
        }

        /* The "Redeemed" Stamp */
        .coupon.redeemed {
            opacity: 0.5;
            filter: sepia(0.5);
            pointer-events: none;
        }

        .coupon.redeemed::before {
            content: "50th GOLDEN USED";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(-15deg);
            font-weight: 900;
            font-size: 1.8rem;
            color: #c0392b;
            border: 5px double #c0392b;
            padding: 5px 15px;
            z-index: 10;
            background: rgba(255, 255, 255, 0.8);
        }

        .icon { 
            font-size: 3.5rem; 
            margin-bottom: 10px; 
            filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
        }

        h3 { 
            margin: 10px 0; 
            font-family: 'Playfair Display', serif;
            color: var(--gold-dark);
            font-size: 1.5rem;
        }

        p { font-size: 0.95rem; line-height: 1.4; color: #666; margin-bottom: 25px; }

        button {
            background: linear-gradient(135deg, var(--gold-mid), var(--gold-dark));
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 50px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(170, 138, 46, 0.3);
            transition: 0.2s;
        }

        button:active { transform: scale(0.95); }

        #status-msg {
            position: fixed;
            bottom: 20px;
            background: #27ae60;
            color: white;
            padding: 12px 25px;
            border-radius: 50px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 100;
        }
    </style>
</head>
<body>

<header>
    <h1>Mama's Golden Voucher</h1>
    <div class="sub-header">Hapyy 50 Years of Life, Ma!</div>
    <p style="margin-top: 15px;">Expiration date? Tidak ada 😏</p>
    <p style="font-size: 0.8rem; color: var(--gold-dark);">Claimable as long as there is no urgent business! 👑</p>
</header>

<div class="grid" id="coupon-grid">
    <!-- Coupons Injected by JS -->
</div>

<div id="status-msg">Voucher Redeemed! Check your email soon, Ma! ✨</div>

<script>
    // 1. REPLACE 'meengrok' WITH YOUR ACTUAL FORMSPREE ID
    const FORMSPREE_ID = "meengrok"; 

    const coupons = [
        { id: 1, icon: "👨🏻‍🍳", title: "Home Cooked Dinner", desc: "Pilih menu favorit Mama, I will do the cooking and the cleaning!" },
        { id: 2, icon: "🥂", title: "Mom - Son Date", desc: "A special outing to a place of your choice. My treat!" },
        { id: 3, icon: "✨", title: "Ask Me Anything", desc: "One hour of tech support, advice, or just chatting. I'm all ears." },
        { id: 4, icon: "🚐", title: "Personal Chauffeur", desc: "I'll be your supir for the whole day. Wherever you need to go." },
        { id: 5, icon: "🧹", title: "Ultimate Cleaning", desc: "I'll handle the heavy cleaning and chores so you can relax." }
    ];

    const grid = document.getElementById('coupon-grid');

    coupons.forEach(c => {
        const card = document.createElement('div');
        card.className = 'coupon';
        card.id = `coupon-${c.id}`;
        card.innerHTML = `
            <div class="icon">${c.icon}</div>
            <h3>${c.title}</h3>
            <p>${c.desc}</p>
            <button onclick="redeem(${c.id}, '${c.title}')">Redeem Voucher</button>
        `;
        grid.appendChild(card);
    });

    async function redeem(id, title) {
        // If ID hasn't been changed from your placeholder
        if (FORMSPREE_ID === "meengrok") {
            alert("Voucher claimed! (Note: Connect Formspree to get actual notifications).");
            document.getElementById(`coupon-${id}`).classList.add('redeemed');
            return;
        }

        try {
            const response = await fetch(`https://formspree.io/f/${FORMSPREE_ID}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ 
                    subject: `Mom's 50th Birthday: Voucher Redeemed!`,
                    message: `Happy 50th! Mama just redeemed: ${title}` 
                })
            });

            if (response.ok) {
                document.getElementById(`coupon-${id}`).classList.add('redeemed');
                const msg = document.getElementById('status-msg');
                msg.style.display = 'block';
                setTimeout(() => msg.style.display = 'none', 4000);
            }
        } catch (error) {
            alert("Connection error. Please try again!");
        }
    }
</script>

</body>
</html>
