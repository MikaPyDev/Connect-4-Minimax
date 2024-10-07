# Connect-4-Minimax
Creating a connect 4 bot using the Minimax algorithm.

This project contains all the python code files you need to make a very strong connect 4 bot, which you can play against. Below I explain the algorithm in detail, including alpha-beta pruning.

### Minimax explanation
The image below shows the main part of the minimax algorithm in pseudo-code with an example on the right. I will use this image in the explanation below.
![image](https://github.com/user-attachments/assets/4c428ed5-f1aa-4440-a58b-9d26ec6c4e98)

After the initial call, the function is called and the following parameters are provided:
- currentPosition: the current game state
- 3: this is the depth, i.e. the number of moves deep it looks at
- true: if it is the maximizingplayer. After having played a move, the minimizingplayer is on and becomes false (when running the algorithm).

If the depth is not 0 and there is no game_over in the passed state (never in the beginning of course) it first executes the piece of code under maximizingplayer, this is the bot.

The maxEval is a very low number at the beginning (-infinity). Then, in a loop, it executes the algorithm for each child. (A child is basically the game state after one of the possible moves has been played).

Even though the function is called again (it is a recursive function), the difference with the previous iteration is that the depth has now gone -1 because a move has been played so you are 1 move deeper (depth = 0 is the deepest). Also, maximizingplayer is now false because the other player (minimizingplayer) is on. Finally, the game state is updated with the played move.

In the example, the same happens now with the minimizingplayer, and then it's the turn of the maximizingplayer again; the depth has now become 1. On the next function call, the static evaluation is returned (called because 1-1=0), which is the score the game state has, -1 in the example.

Then we arrived at the line under the maximising player that chooses the max between -infinity and the score -1 (the first time, of course, is always the score).

Then the loop now explores the 2nd child, depth = 1 was remembered in this recursive iteration and on the new function call the depth becomes 1-1=0 again. So again the static evaluation is returnt, 3 in the example.

Then the max is chosen between -1 and 3 by the maximizingplayer, that number (3) is then returned to the minimizingplayer. He checks the minEval and then it goes to its 2nd child (loop).

Since the depth here was 2, it goes to 2-1=1 and the maximizingplayer is executed again. Depth becomes 1-1=0 so it returns the static evaluation but that's all explained above. This process continues and so eventually the max is chosen in the original game state. After that, the corresponding move is executed in the real game.

Obvious questions:
- How are the children obtained?? Those are just the game states after the possible moves.
- How is the score calculated? For example, that's 100 for 4 in a row, 8 for 3 in a row and 2 for 2 in a row. Points added up - the opponent's points = the score.
- Is a score function always executed? No, only at depth = 0 because then a static evaluation comes up.

### Alpha-Beta pruning explanation
Going through all possible moves takes quite a long time, especially in games with many possible moves or a high initial depth. That's why pruning is used to save a lot of time.

I used alpha-beta pruning. Branches (with nodes attached) that will never be chosen won't be explored: the loop is aborted. This is because a better option has already been explored in such a situation.  Below is the above image supplemented by the prune piece.
![image](https://github.com/user-attachments/assets/0902aeb8-9bae-4e83-a274-bfc282fbc886)

The new process is very similar to the one just described so I start my explanation right at the white node at the bottom left, this is the maximizingplayer (he only changes the alpha value!). 

The static evaluation -1 (the score) has been received. Now alpha becomes the max of -infinity and the received score, the first time of course it is always the score. 

Then it goes to the 2nd child and a score of 3 is received. The maximizingplayer now chooses the max between -1 and the new score, so alpha now changes to 3. 

Then you come back to the minimizingplayer (which only changes the beta value!). It chooses the minimum of the score (3) and +infinity, which of course is always the score the first time. So beta becomes 3 and then he goes to his 2nd child, the maximizingplayer. 

The difference with his 1st child is that he now passes the beta (3) that is already known (not the alpha because he remembers the alpha from his own recursive iteration and it was still at -infinity there, this is the same principle as used with depth). 

The 1st child of the maximizingplayer has score 5. Since that is greater than -infinity, alpha becomes 5. Here's the thing: the condition beta < alpha is true now so it breaks the loop and will not explore its 2nd child (or all children thereafter in a situation with multiple children). This is because white (maximizingplayer) chooses the highest score and so it will now be 5 (maybe even higher if he had continued the loop). The beta (the option black as minimizingplayer prefers to choose so far) is smaller than 5, namely 3. So he will always go for that 3, which means that the 2nd child no longer needs to be explored. 

In other words to summarise: white chooses the highest, so 5 or higher, and black the lowest, so 3 in this case because the 2nd child will never again be able to supply a number lower than 3. This process continues like this all the time.

Obvious question:
- maxEval picks the max and then alpha also. Can't maxEval be used as alpha? No, because maxEval has to be reset at each recursive iteration, alpha is remembered and passed (down the tree).

### Is it unbeatable?
Coming soon

### Other useful information:
The code folder contains 2 files:
  1. Connect4S: the game. Start this file if you want to play against a friend (uncomment line 40 for this);
  2. MinimaxS: the controller with the algorithm. Start this file if you want to play against the algorithm.

The main libraries from this project are:
  1. Numpy
  2. Pygame

Finally, I would like to thank SebastianLague for the clear images:
  - https://www.youtube.com/@SebastianLague
