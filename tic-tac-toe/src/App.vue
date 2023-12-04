<template>
    <main class>
        <h1>Tic Tac Toe</h1>
        <h3>Player {{ player }}'s turn</h3>
        <div class="board-wrapper">
            <div class="row"
                v-for="(row, x) in board"
                :key="x">
                <div class="ceil"
                    v-for="(ceil, y) in row"
                    :key="y" @click="makemove(x, y)">
                    {{ ceil === 'X' ? 'X': ceil === 'O' ? 'O' : ''}}
                </div>
            </div>
        </div>
        <h2 v-if="winner">Player '{{ winner }} wins!'</h2>
        <button @click="resetGame">Reset Game</button>
    </main>
</template>

<script setup>
import {ref, computed} from 'vue'

const player = ref('X');
const board = ref([['', '', ''],
                   ['', '', ''],
                   ['', '', '']])

function calculateWinner(squares){
    const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
];

    for(let i = 0; i<lines.length; i++){
        const [a,b,c] = lines[i];
        if(squares[a] && squares[a] === squares[b] && squares[a] === squares[c]){
            return squares[a];
        }
    }
    return null;
}

const winner = computed(() => calculateWinner(board.value.flat()))

const makemove = (x, y) =>{
    if(winner.value) return 

    if(board.value[x][y] != '') return

    board.value[x][y] = player.value

    player.value = player.value === 'X' ? 'O' : 'X'
}


const resetGame = () =>{
    board.value = [['', '', ''],
                   ['', '', ''],
                   ['', '', '']]
    player.value = 'X';
}
</script>

<style>
*{
    font-family: Verdana, Geneva, Tahoma, sans-serif;
}
main{
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.board-wrapper{
    width: 300px;
    height: 300px;
}
.ceil{
    width: 100px;
    height:100px;
    border: 1px solid #777;
    display: flex;
    font-size: 50px;
    color: #fff;
    align-items: center;
    justify-content: center;
    transition: 0.3s;
}
.ceil:hover{
    background-color:rgb(45, 43, 43);
}
.row{
    widows: 100px;
    height: 100px;
    border: 1px solid rgb(17, 16, 16);
    position: relative;
    display: flex;
}
h1, h2, h3{
    color: #fff;
    text-align: center;
}
button{
    position: relative;
    padding: 7px;
    margin: 20px;
}
</style>