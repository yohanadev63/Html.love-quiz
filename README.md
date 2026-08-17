# Html.love-quiz
    let name = "";
    let heartInterval;

    const step1 = document.getElementById("step1");
    const step2 = document.getElementById("step2");
    const step3 = document.getElementById("step3");
    const step4 = document.getElementById("step4");
    const step5 = document.getElementById("step5");

    const nameInput = document.getElementById("nameInput");
    const question = document.getElementById("question");
    const customMsg = document.getElementById("customMsg");

    const noBtn = document.getElementById("noBtn");
    const moneyNoBtn = document.getElementById("moneyNoBtn");


    // STEP 1
    function startQuiz() {
        name = nameInput.value.trim();

        if (name === "") {
            alert("Acha ujinga 😂 Weka jina kwanza ❤️");
            nameInput.focus();
            return;
        }

        question.innerText =
            `Hi ${name}, do you love me? 😳❤️`;

        step1.classList.add("hidden");
        step2.classList.remove("hidden");

        positionNoButton();
    }


    // LOVE QUESTION - NO BUTTON
    function runAway() {
        positionNoButton();
    }


    function positionNoButton() {
        const buttonWidth = noBtn.offsetWidth || 100;
        const buttonHeight = noBtn.offsetHeight || 50;

        const maxX = Math.max(
            10,
            window.innerWidth - buttonWidth - 10
        );

        const maxY = Math.max(
            10,
            window.innerHeight - buttonHeight - 10
        );

        const x = Math.random() * maxX;
        const y = Math.random() * maxY;

        noBtn.style.left = `${x}px`;
        noBtn.style.top = `${y}px`;
    }


    // SHE SAYS YES TO LOVE
    function sayYes() {
        step2.classList.add("hidden");
        step3.classList.remove("hidden");

        customMsg.innerText =
            `${name}, you just made my day! ❤️`;

        createHearts();
    }


    // SHOW MONEY QUESTION
    function showMoneyQuestion() {
        step3.classList.add("hidden");
        step4.classList.remove("hidden");

        positionMoneyNoButton();
    }


    // MONEY NO BUTTON ESCAPES 😂
    function runMoneyNo() {
        positionMoneyNoButton();
    }


    function positionMoneyNoButton() {
        const buttonWidth = moneyNoBtn.offsetWidth || 100;
        const buttonHeight = moneyNoBtn.offsetHeight || 50;

        const maxX = Math.max(
            10,
            window.innerWidth - buttonWidth - 10
        );

        const maxY = Math.max(
            10,
            window.innerHeight - buttonHeight - 10
        );

        const x = Math.random() * maxX;
        const y = Math.random() * maxY;

        moneyNoBtn.style.left = `${x}px`;
        moneyNoBtn.style.top = `${y}px`;
    }


    // SHE CLICKS YES TO MONEY
    function moneyYes() {
        step4.classList.add("hidden");
        step5.classList.remove("hidden");

        createHearts();
    }


    // FALLING HEARTS ❤️
    function createHearts() {
        if (heartInterval) {
            clearInterval(heartInterval);
        }

        heartInterval = setInterval(() => {
            const heart = document.createElement("div");

            heart.classList.add("hearts");

            const hearts = [
                "❤️",
                "💕",
                "💖",
                "💗",
                "💓",
                "💘",
                "🥰"
            ];

            heart.innerText =
                hearts[Math.floor(Math.random() * hearts.length)];

            heart.style.left =
                Math.random() * 100 + "vw";

            heart.style.top = "-50px";

            heart.style.fontSize =
                (20 + Math.random() * 25) + "px";

            heart.style.animationDuration =
                (2 + Math.random() * 3) + "s";

            document.body.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 5000);

        }, 200);
    }


    // RESTART
    function restart() {
        if (heartInterval) {
            clearInterval(heartInterval);
            heartInterval = null;
        }

        document.querySelectorAll(".hearts").forEach(heart => {
            heart.remove();
        });

        nameInput.value = "";

        step2.classList.add("hidden");
        step3.classList.add("hidden");
        step4.classList.add("hidden");
        step5.classList.add("hidden");

        step1.classList.remove("hidden");
    }


    // ENTER KEY
    nameInput.addEventListener("keydown", function(event) {
        if (event.key === "Enter") {
            startQuiz();
        }
    });


    // KEEP BUTTONS INSIDE SCREEN
    window.addEventListener("resize", function() {
        if (!step2.classList.contains("hidden")) {
            positionNoButton();
        }

        if (!step4.classList.contains("hidden")) {
            positionMoneyNoButton();
        }
    });
</script>
