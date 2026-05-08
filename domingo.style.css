<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dominó - 4 Jugadores</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    background:#14532d;
    overflow:hidden;
    color:white;
}

/* TÍTULO */

h1{
    position:absolute;
    top:8px;
    left:50%;
    transform:translateX(-50%);
    font-size:28px;
    z-index:20;
    background:rgba(0,0,0,0.35);
    padding:8px 18px;
    border-radius:12px;
}

/* TABLERO */

#board{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    width:82%;
    height:38%;
    background:#1f7a3f;
    border-radius:18px;
    border:4px solid rgba(255,255,255,0.2);

    display:flex;
    align-items:center;
    justify-content:center;
    gap:4px;

    padding:8px;
    overflow:auto;
}

/* JUGADORES */

.player-area{
    position:absolute;
    display:flex;
    gap:4px;
    justify-content:center;
    align-items:center;
}

#player{
    bottom:18px;
    left:50%;
    transform:translateX(-50%);
}

#cpu1{
    top:80px;
    left:50%;
    transform:translateX(-50%);
}

#cpu2{
    left:18px;
    top:50%;
    transform:translateY(-50%);
    flex-direction:column;
}

#cpu3{
    right:18px;
    top:50%;
    transform:translateY(-50%);
    flex-direction:column;
}

/* FICHAS */

.domino{
    background:white;
    border:2px solid black;
    border-radius:8px;
    overflow:hidden;
    display:flex;
    color:black;
    font-weight:bold;
    cursor:pointer;
    transition:0.15s;
}

.domino:hover{
    transform:scale(1.05);
}

.vertical{
    flex-direction:column;
    width:42px;
    height:84px;
}

.horizontal{
    flex-direction:row;
    width:84px;
    height:42px;
}

.half{
    flex:1;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:18px;
}

.vertical .half{
    border-bottom:2px solid black;
}

.vertical .half:last-child{
    border-bottom:none;
}

.horizontal .half{
    border-right:2px solid black;
}

.horizontal .half:last-child{
    border-right:none;
}

.back{
    background:#222;
    border:2px solid #444;
}

/* INFO */

#info{
    position:absolute;
    bottom:120px;
    left:50%;
    transform:translateX(-50%);
    background:rgba(0,0,0,0.5);
    padding:10px 16px;
    border-radius:10px;
    font-size:18px;
}

/* GANADOR */

#winnerScreen{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.75);
    display:none;
    justify-content:center;
    align-items:center;
    z-index:999;
    animation:fadeIn 0.5s;
}

#winnerBox{
    background:white;
    color:black;
    padding:40px;
    border-radius:20px;
    text-align:center;
    animation:pop 0.6s ease;
}

#winnerBox h2{
    font-size:42px;
    margin-bottom:10px;
}

#winnerBox p{
    font-size:24px;
}

/* BOTÓN GANADOR */

#restartWinnerBtn{
    margin-top:20px;
    padding:12px 24px;
    border:none;
    border-radius:12px;
    background:#22c55e;
    color:white;
    font-size:18px;
    font-weight:bold;
    cursor:pointer;
    transition:0.2s;
}

#restartWinnerBtn:hover{
    transform:scale(1.05);
    background:#16a34a;
}

/* ANIMACIONES */

@keyframes pop{

    0%{
        transform:scale(0.3) rotate(-10deg);
        opacity:0;
    }

    60%{
        transform:scale(1.1) rotate(5deg);
    }

    100%{
        transform:scale(1) rotate(0deg);
        opacity:1;
    }
}

@keyframes fadeIn{

    from{
        opacity:0;
    }

    to{
        opacity:1;
    }
}

/* BOTONES */

.controls{
    position:absolute;
    top:10px;
    right:10px;
    display:flex;
    gap:10px;
}

button{
    padding:10px 18px;
    border:none;
    border-radius:10px;
    background:#22c55e;
    color:white;
    cursor:pointer;
    font-weight:bold;
}

button:hover{
    background:#16a34a;
}

#drawBtn{
    background:#f59e0b;
}

#drawBtn:hover{
    background:#d97706;
}

</style>
</head>
<body>

<h1>Dominó - Empieza la Mula de 6</h1>

<div id="board"></div>

<div id="cpu1" class="player-area"></div>
<div id="cpu2" class="player-area"></div>
<div id="cpu3" class="player-area"></div>

<div id="player" class="player-area"></div>

<div id="info">
    Buscando mula de 6...
</div>

<!-- PANTALLA GANADOR -->

<div id="winnerScreen">

    <div id="winnerBox">

        <h2>
            🎉 GANADOR 🎉
        </h2>

        <p id="winnerText"></p>

        <button id="restartWinnerBtn" onclick="startGame()">
            Jugar otra vez
        </button>

    </div>

</div>

<!-- BOTONES -->

<div class="controls">

    <button id="drawBtn" onclick="drawPiece()">
        Robar ficha
    </button>

    <button onclick="startGame()">
        Reiniciar
    </button>

</div>

<script>

/* VARIABLES */

let deck = [];
let board = [];

let players = [
    {name:"Jugador", hand:[], cpu:false},
    {name:"CPU 1", hand:[], cpu:true},
    {name:"CPU 2", hand:[], cpu:true},
    {name:"CPU 3", hand:[], cpu:true}
];

let currentPlayer = 0;

/* CREAR MAZO */

function createDeck(){

    deck = [];

    for(let i=0;i<=6;i++){

        for(let j=i;j<=6;j++){

            deck.push([i,j]);
        }
    }

    /* MÁS FICHAS */

    let extra = [...deck];

    deck = deck.concat(extra);
    deck = deck.concat(extra);

    shuffle(deck);
}

/* MEZCLAR */

function shuffle(array){

    for(let i=array.length-1;i>0;i--){

        let j = Math.floor(Math.random()*(i+1));

        [array[i],array[j]] = [array[j],array[i]];
    }
}

/* REPARTIR */

function dealCards(){

    players.forEach(player=>{

        player.hand = [];

        for(let i=0;i<7;i++){

            player.hand.push(deck.pop());
        }
    });
}

/* CREAR FICHA */

function createDomino(piece, hidden=false, rotation="vertical"){

    const domino = document.createElement("div");

    domino.className = "domino " + rotation;

    if(hidden){

        domino.classList.add("back");

        return domino;
    }

    const top = document.createElement("div");
    top.className = "half";
    top.textContent = piece[0];

    const bottom = document.createElement("div");
    bottom.className = "half";
    bottom.textContent = piece[1];

    domino.appendChild(top);
    domino.appendChild(bottom);

    return domino;
}

/* MOSTRAR MANOS */

function renderHands(){

    document.getElementById("player").innerHTML = "";
    document.getElementById("cpu1").innerHTML = "";
    document.getElementById("cpu2").innerHTML = "";
    document.getElementById("cpu3").innerHTML = "";

    players.forEach((player,index)=>{

        const area =
            document.getElementById(
                index===0 ? "player" :
                index===1 ? "cpu1" :
                index===2 ? "cpu2" :
                "cpu3"
            );

        player.hand.forEach((piece,pieceIndex)=>{

            let domino;

            if(player.cpu){

                domino = createDomino(piece,true);

            }else{

                domino = createDomino(piece,false);

                if(currentPlayer===0){

                    domino.onclick = ()=>playPiece(pieceIndex);
                }
            }

            area.appendChild(domino);
        });
    });
}

/* MOSTRAR TABLERO */

function renderBoard(){

    const boardDiv = document.getElementById("board");

    boardDiv.innerHTML = "";

    board.forEach(data=>{

        const domino = createDomino(
            data.piece,
            false,
            data.rotation
        );

        domino.style.cursor = "default";

        boardDiv.appendChild(domino);
    });
}

/* PUEDE JUGAR */

function canPlay(piece){

    if(board.length===0) return true;

    let left = board[0].piece[0];
    let right = board[board.length-1].piece[1];

    return (
        piece[0]===left ||
        piece[1]===left ||
        piece[0]===right ||
        piece[1]===right
    );
}

/* COLOCAR */

function placePiece(piece){

    let rotation =
        piece[0]===piece[1]
        ? "vertical"
        : "horizontal";

    if(board.length===0){

        board.push({
            piece:piece,
            rotation:rotation
        });

        return true;
    }

    let left = board[0].piece[0];
    let right = board[board.length-1].piece[1];

    if(piece[1]===left){

        board.unshift({
            piece:piece,
            rotation:rotation
        });

    }
    else if(piece[0]===left){

        board.unshift({
            piece:[piece[1],piece[0]],
            rotation:rotation
        });

    }
    else if(piece[0]===right){

        board.push({
            piece:piece,
            rotation:rotation
        });

    }
    else if(piece[1]===right){

        board.push({
            piece:[piece[1],piece[0]],
            rotation:rotation
        });

    }
    else{

        return false;
    }

    return true;
}

/* GANADOR */

function showWinner(playerName){

    document.getElementById("winnerScreen").style.display =
        "flex";

    document.getElementById("winnerText").textContent =
        playerName + " se quedó sin fichas 🎉";
}

/* REVISAR GANADOR */

function checkWinner(player){

    if(player.hand.length===0){

        document.getElementById("info").textContent =
            player.name + " ganó";

        showWinner(player.name);

        return true;
    }

    return false;
}

/* JUGADOR */

function playPiece(index){

    if(currentPlayer!==0) return;

    let player = players[0];

    let piece = player.hand[index];

    if(placePiece(piece)){

        player.hand.splice(index,1);

        renderBoard();
        renderHands();

        if(checkWinner(player)) return;

        nextTurn();
    }
}

/* ROBAR */

function drawPiece(){

    if(currentPlayer!==0) return;

    if(deck.length<=0){

        document.getElementById("info").textContent =
            "No quedan fichas";

        return;
    }

    players[0].hand.push(deck.pop());

    renderHands();

    document.getElementById("info").textContent =
        "Robaste una ficha";
}

/* SIGUIENTE TURNO */

function nextTurn(){

    currentPlayer = (currentPlayer + 1) % 4;

    updateInfo();

    if(players[currentPlayer].cpu){

        setTimeout(cpuPlay,900);
    }
}

/* CPU */

function cpuPlay(){

    let cpu = players[currentPlayer];

    for(let i=0;i<cpu.hand.length;i++){

        if(canPlay(cpu.hand[i])){

            placePiece(cpu.hand[i]);

            cpu.hand.splice(i,1);

            renderBoard();
            renderHands();

            if(checkWinner(cpu)) return;

            nextTurn();

            return;
        }
    }

    if(deck.length>0){

        cpu.hand.push(deck.pop());

        renderHands();
    }

    nextTurn();
}

/* INFO */

function updateInfo(){

    document.getElementById("info").textContent =
        "Turno de: " + players[currentPlayer].name;
}

/* BUSCAR MULA DE 6 */

function findDoubleSixStarter(){

    for(let i=0;i<players.length;i++){

        for(let j=0;j<players[i].hand.length;j++){

            let piece = players[i].hand[j];

            if(piece[0]===6 && piece[1]===6){

                currentPlayer = i;

                players[i].hand.splice(j,1);

                board.push({
                    piece:[6,6],
                    rotation:"vertical"
                });

                renderBoard();
                renderHands();

                document.getElementById("info").textContent =
                    players[i].name + " empezó con la mula de 6";

                return;
            }
        }
    }
}

/* INICIAR */

function startGame(){

    document.getElementById("winnerScreen").style.display =
        "none";

    createDeck();

    board = [];

    dealCards();

    renderHands();

    findDoubleSixStarter();

    setTimeout(()=>{

        nextTurn();

    },1000);
}

startGame();

</script>

</body>
</html>