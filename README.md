# manvendra2512
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Perfect Center Strike</title>

<style>
body {
    background: #111;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    position: relative;
}

/* Board */
.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 5px;
}

.cell {
    width: 100px;
    height: 100px;
    background: #222;
    display: flex;
    justify-content: center;
    align-items: center;
}

/* X */
.line {
    stroke: #00f5d4;
    stroke-width: 6;
    stroke-dasharray: 100;
    stroke-dashoffset: 100;
    animation: draw 0.5s forwards;
}

/* O */
.circle {
    stroke: #f15bb5;
    stroke-width: 6;
    fill: none;
    stroke-dasharray: 300;
    stroke-dashoffset: 300;
    animation: draw 0.7s forwards;
}

/* Outside circle aligned exactly */
.outside {
    position: absolute;
    left: 360px;
    top: 360px; /* adjusted to lie exactly on diagonal */
}

/* Strike */
.strike {
    position: absolute;
    top: 0;
    left: 0;
}

.strike line {
    stroke: yellow;
    stroke-width: 6;
    stroke-dasharray: 600;
    stroke-dashoffset: 600;
    animation: draw 1.2s forwards;
    animation-delay: 3s;
}

@keyframes draw {
    to {
        stroke-dashoffset: 0;
    }
}
</style>
</head>

<body>

<div class="container">

    <div class="board" id="board"></div>

    <!-- Outside Circle -->
    <div class="outside" id="outsideCircle"></div>

    <!-- PERFECT DIAGONAL THROUGH CENTERS -->
    <svg class="strike" width="500" height="500">
        <!-- center (155,155) → bottom-right (255,255) → outside -->
        <line x1="155" y1="155" x2="415" y2="415"></line>
    </svg>

</div>

<script>
const board = document.getElementById("board");
const outside = document.getElementById("outsideCircle");

const pattern = [
    "X","O","X",
    "X","O","X",
    "O","X","O"
];

pattern.forEach((val, i) => {
    const cell = document.createElement("div");
    cell.classList.add("cell");

    setTimeout(() => {
        if (val === "X") {
            cell.innerHTML = `
            <svg width="60" height="60">
                <line x1="10" y1="10" x2="50" y2="50" class="line"/>
                <line x1="50" y1="10" x2="10" y2="50" class="line"/>
            </svg>`;
        } else {
            cell.innerHTML = `
            <svg width="60" height="60">
                <circle cx="30" cy="30" r="20" class="circle"/>
            </svg>`;
        }
    }, i * 250);

    board.appendChild(cell);
});

/* Outside circle */
setTimeout(() => {
    outside.innerHTML = `
    <svg width="60" height="60">
        <circle cx="30" cy="30" r="20" class="circle"/>
    </svg>`;
}, 2200);
</script>

</body>
</html>
