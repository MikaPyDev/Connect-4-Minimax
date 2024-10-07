# Connect-4-Minimax
Creating a connect 4 bot using the Minimax algorithm.

This project contains all the python code files you need to make a strong connect 4 bot, which you can play against. Below I explain the algorithm in detail, including alpha-beta pruning.

### Minimax explanation
The image below shows the main part of the minimax algorithm in pseudo-code with an example on the right. I will use this image in the explanation below.
![image](https://github.com/user-attachments/assets/4c428ed5-f1aa-4440-a58b-9d26ec6c4e98)
After the initial call, the function is called and the following parameters are provided:
- currentPosition: the current game state
- 3: this is the depth, i.e. the number of moves deep it looks at
- true: if it is the maximisingplayer. After having played a move, the minimisingplayer is on and becomes false (when running the algorithm).
If the depth is not 0 and there is no game_over in the passed state (never in the beginning of course) it first executes the piece of code under maximisingplayer, this is the bot.
The maxEval is a very low number at the beginning (-infinity). Then, in a loop, it executes the algorithm for each child. (A child is basically the game state after one of the possible moves has been played).
Even though the function is called again (it is a recursive function), the difference with the previous iteration is that the depth has now gone -1 because a move has been played so you are 1 move deeper (depth = 0 is the deepest). Also, maximisingplayer is now false because the other player (minimisingplayer) is on. Finally, the game state is updated with the played move.
In the example, the same happens now with the minimisingplayer, and then it's the turn of the maximisingplayer again; the depth has now become 1. On the next function call, the static evaluation is returned (called because 1-1=0), which is the score the game state has, -1 in the example.
Then we arrived at the line under the maximising player that chooses the max between -infinity and the score -1 (the first time, of course, is always the score).
Then the loop now explores the 2nd child, depth = 1 was remembered in this recursive iteration and on the new function call the depth becomes 1-1=0 again. So again the static evaluation is retried, 3 in the example.
Then the max is chosen between -1 and 3 by the maximising player, that number (3) is then returned to the minimising player. That checks the minEval and then it goes to its 2nd child (loop).
Since the depth here was 2, it goes to 2-1=1 and the maximisingplayer is executed again. Depth becomes 1-1=0 so it returns the static evaluation but that's all explained above. This process continues and so eventually the max is chosen in the original game state after which the corresponding move is executed in the real game.



Translated with DeepL.com (free version)

### Source
I want to thank:
https://www.youtube.com/@SebastianLague
