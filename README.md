<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: SAI VISHAL D</h3>
<h3>Register Number: 212223230180</h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

### Program:
```
#Tic-Tac-Toe board
class Board:
    def __init__(self):
        self.board = [' ' for _ in range(9)]

    def available_moves(self):
        return [i for i, spot in enumerate(self.board) if spot == ' ']

    def make_move(self, move, player):
        self.board[move] = player

    def is_winner(self, player):
        winning_combos = [[0, 1, 2], [3, 4, 5], [6, 7, 8],
                          [0, 3, 6], [1, 4, 7], [2, 5, 8],
                          [0, 4, 8], [2, 4, 6]]
        for combo in winning_combos:
            if all(self.board[i] == player for i in combo):
                return True
        return False

    def is_full(self):
        return ' ' not in self.board

    def print_board(self):
        for i in range(0, 9, 3):
            print('|'.join(self.board[i:i+3]))
            if i < 6:
                print('-' * 5)

#Minimax algorithm with alpha-beta pruning
def minimax(board, depth, player, alpha, beta):
    if board.is_winner('X'):
        return -1
    elif board.is_winner('O'):
        return 1
    elif board.is_full():
        return 0

    if player == 'O':
        best_val = float('-inf')
        for move in board.available_moves():
            board.make_move(move, player)
            value = minimax(board, depth + 1, 'X', alpha, beta)
            board.make_move(move, ' ')
            best_val = max(best_val, value)
            alpha = max(alpha, best_val)
            if beta <= alpha:
                break
        return best_val
    else:
        best_val = float('inf')
        for move in board.available_moves():
            board.make_move(move, player)
            value = minimax(board, depth + 1, 'O', alpha, beta)
            board.make_move(move, ' ')
            best_val = min(best_val, value)
            beta = min(beta, best_val)
            if beta <= alpha:
                break
        return best_val

#Find the best move for the AI player using minimax with alpha-beta pruning
def find_best_move(board):
    best_move = -1
    best_val = float('-inf')
    alpha = float('-inf')
    beta = float('inf')

    for move in board.available_moves():
        board.make_move(move, 'O')
        value = minimax(board, 0, 'X', alpha, beta)
        board.make_move(move, ' ')
        if value > best_val:
            best_val = value
            best_move = move
        alpha = max(alpha, best_val)
    return best_move

#Main function to play the game
def play_game():
    board = Board()
    current_player = 'X'

    while True:
        board.print_board()

        if current_player == 'X':
            move = int(input("Enter your move (0-8): "))
            if move not in board.available_moves():
                print("Invalid move. Try again.")
                continue
        else:
            move = find_best_move(board)
            print(f"AI plays move: {move}")

        board.make_move(move, current_player)

        if board.is_winner(current_player):
            board.print_board()
            print(f"{current_player} wins!")
            break
        elif board.is_full():
            board.print_board()
            print("It's a tie!")
            break

        current_player = 'O' if current_player == 'X' else 'X'

#Play the game
play_game()

```
### Result:
Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game has been implemented successfully.
