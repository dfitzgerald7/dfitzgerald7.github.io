---
layout: post
title:      "Integrating a chess database api into my React project."
date:       2019-03-03 22:13:48 +0000
permalink:  integrating_a_chess_database_api_into_my_react_project
---


I have recently been getting back into playing chess. For my final project, I decided that it would be worthwhile to create some sort of chess training app. My initial idea was to integrate a chess engine and be able to play games against that. I searched for an api that could recieve a post request with a chess position and would return a move. While there are different ways to add an engine such as Stockfish to an app, I felt it was out of the scope of the requirements and not worthwhile. 

After searching for engine apis, I found one that could recieve a get request with a FEN position and return a professional game with that same opening. FEN is a standard notation that looks something like 
```
"rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"
```
to represent the board and turn number. Now, I faced two problems. First, how to actually display and use a chess board in my app. Second, how to use the data from the fetch request to display the game. 

Luckily, I found two popular chess packages, Chess.js which contained the logic of chess and Chessboard.jsx that contained a board component. These two made it relatively simple to just integrate a chessboard that could play a game with two users. Now it was time to import a game. The response from the api was not JSON, and would look something like 
```
[Event "Wch Blitz"]
[Site "Astana"]
[Date "2012.07.10"]
[Round "23"]
[White "Carlsen, Magnus"]
[Black "Chadaev, Nikolay"]
[Result "1-0"]
[WhiteElo "2837"]
[BlackElo "2580"]

1. e4 e5 2. f4 d5 3. exd5 exf4 4. Nf3 Nf6 5. c4 c6 6. d4 cxd5 7. c5 Nc6 8. Bb5 Be7 9. O-O O-O 10. Bxf4 ...
```

To make this a useable move list, I did
```
      const moveList = action.payload.split("\n").slice(-1)[0]
      const cleanMoveList = moveList.replace(/\d+\. /g, "").split(" ")
```
where cleanMoveList is an array of just the moves. So we have a response but have one more issue. The chessboard.jsx component requires FEN notation to display a position, but the response from the professional game is just a move list. This is where we use Chess.js. I instantiated a chess class outside of my container component. 
```
import Chess from "chess.js";

const chess = new Chess();
```
This instance has two methods, move(), which takes a move and applys that to the game, and fen(), which return the FEN position of the game. Using both Chess.js and Chessboard.jsx, the flow is: 
1. Click a button for the next move from the fetched game.
2. Find that move from the fetched move array using the current move as the index.
3. Input that move into the chess instance.
4. Retrieve that FEN position from the chess instance.
5. Display that move by passing that FEN to the chessboard component. 

Now, we can play out an entire professional game. 

