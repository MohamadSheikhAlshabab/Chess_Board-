# Lab: 11 - Numpy¶

---
## import the libraries : numpy, matplotlib:¶
<pre>
import matplotlib.pyplot as plt
import numpy as np
</pre>
---
### Create Class Called ChessBoard:¶
<pre>
class ChessBoard:
    white = [1,1,1]
    blue = [0,0,1]
    red = [1,0,0]
    queen_red=None
    queen_blue=None
    x_red=None
    y_red=None
    x_blue=None
    y_blue=None
    under_attack=True   
    
    def __init__(self):
        # Create the board (grid)
        self.grid = np.zeros([8,8,3])
        # self.grid = np.random.rand(8,8,3)
        for i in range(8):
            for j in range(8):
                if (i%2==0 and j%2==0) or (i%2==1 and j%2==1):
                    self.grid[i,j] = ChessBoard.white
    
          
    def render(self):
        plt.imshow(self.grid)

    def add_red(self,row,col):
        self.grid[row,col]=ChessBoard.red
        ChessBoard.x_red=row
        ChessBoard.y_red=col
        ChessBoard.queen_red=[row,col]
        self.render()

    def add_blue(self,row,col):
        self.grid[row,col]=ChessBoard.blue
        ChessBoard.x_blue=row
        ChessBoard.y_blue=col
        ChessBoard.queen_blue=[row,col]
        self.render()
        
    def check_if_under_attack(self,x_red,y_red,x_blue,y_blue):
        """
        To check if the Queen is Under
        attck or Not.
        """
        ChessBoard.x_red=x_red
        ChessBoard.y_red=y_red
        ChessBoard.x_blue=x_blue
        ChessBoard.y_blue=y_blue
        return self.is_under_attack(x_red,y_red,x_blue,y_blue)


    def is_under_attack(self,x_red,y_red,x_blue,y_blue):
        """
        This method is to check if a given coordinates of a blue and red queen will attack each other
        """
        x_subtraction=abs(ChessBoard.x_red-ChessBoard.x_blue)
        y_subtraction=abs(ChessBoard.y_red-ChessBoard.y_blue)

        if  ChessBoard.x_red==ChessBoard.x_blue:
            ChessBoard.under_attack=True
            return ChessBoard.under_attack

        elif ChessBoard.y_red==ChessBoard.y_blue:
            ChessBoard.under_attack=True
            return ChessBoard.under_attack

        elif x_subtraction==y_subtraction:
                ChessBoard.under_attack=True
                return ChessBoard.under_attack

        else:
            ChessBoard.under_attack = False
            return ChessBoard.under_attack
  </pre>
 ----
### create instance for class and test all methods it, and assert them¶

<pre>
chess=ChessBoard()
chess.render()
chess.add_red(4,7)
chess.add_blue(3,7)
assert chess.check_if_under_attack(3,5,4,6) == True #Diagonal check
assert chess.check_if_under_attack(4,5,4,6) == True #Horizontal check
assert chess.check_if_under_attack(3,6,4,6) == True # Vertical check
assert chess.check_if_under_attack(0,0,2,6) == False #Not Under Attack 
</pre>
----
print('All tests passed!!!!!!')
All tests passed!!!!!!
