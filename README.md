# Tic-Tac-Toe-game
#include<iostream>
#include<windows.h> // to access windows library 
using namespace std;

// Abstract Class = Virtual Function 
// Pure Abstract Class = Pure Virtual Function 
// Pure Abstract Class = Interface 

// Encapsulation : Pure Abstract Class
class TicTacToe{
	public:
	
	// when we enter value it should print char i.e why we made it char from int
	char board[3][3]={{'1','2','3'},{'4','5','6'},{'7','8','9'}}; 
	char turn = 'X'; 
	int row ,column;
	bool draw = false;
	HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE);
	
	// Abstraction : pure virtual function 
	virtual void display_board() = 0;
	virtual void player_turn() = 0;
	virtual bool gameover() = 0;
	
};

class Player : public TicTacToe{
	
	public:
		// Implementations of virtual function
	virtual void display_board(){
		
		system("cls");   //to clear and update
	           SetConsoleTextAttribute(h,13);
			cout<<" \t------ T i c k ------ C r o s s ------- G a m e ------ "<<endl<<endl;
			
		cout<<"\tPlayer1[X] \n\tPlayer2[0]"<<endl;
		
		cout<<" \t\t\t     |     |      "<<endl;
		cout<<" \t\t\t  "<<board[0][0]<<"  |  "<<board[0][1]<<"  |  "<<board[0][2]<<"      "<<endl;
		cout<<" \t\t\t_____|_____|_____ "<<endl;
		cout<<" \t\t\t     |     |      "<<endl;
		cout<<" \t\t\t  "<<board[1][0]<<"  |  "<<board[1][1]<<"  |  "<<board[1][2]<<"      "<<endl;
		cout<<" \t\t\t_____|_____|_____ "<<endl;
		cout<<" \t\t\t     |     |      "<<endl;
		cout<<" \t\t\t  "<<board[2][0]<<"  |  "<<board[2][1]<<"  |  "<<board[2][2]<<"      "<<endl;
		cout<<" \t\t\t     |     |      "<<endl;
	}
	
	// Implementations of virtual functions 
	virtual void player_turn(){
	
		int choice;
		
		if( turn == 'X') cout << "\tPlayer1 [X] turn :   " ;
		
		if( turn == '0') cout << "\tPlayer2 [0] turn :   " ;
		cout << endl << " \tEnter Your Choice : " ;
		cin>>choice;
			
		switch(choice){
			
            case 1: 
				row = 0 ; 
				column = 0; 
				break;
				
            case 2: 
				row = 0 ; 
				column = 1; 
				break;  
				                  			    	
			case 3: 
				row = 0 ; 
				column = 2; 
				break;
			
			case 4: 
				row = 1 ; 
				column = 0; 
				break;
				
			case 5: 
				row = 1 ; 
				column = 1; 
				break;
				
			case 6: 
				row = 1 ; 
				column = 2; 
				break;
				
			case 7: 
				row = 2 ; 
				column = 0; 
				break;	 
				
			case 8: 
				row = 2 ; 
				column = 1; 
				break;
				
			case 9: 
				row = 2 ; 
				column = 2; 
				break;
			
			default:
				cout<<"Invalid choice "<<endl;
				break;		
		}
		
		if(turn == 'X' && board[row][column] != 'X' && board[row][column] != '0'){   
		    //condition for not replace again and again i.e we add more condition with turn 
			board[row][column] = 'X';
			turn ='0';
		}
		else if( turn == '0'&& board[row][column] != 'X' && board[row][column] != '0'){
			board[row][column] = '0';
			turn ='X';
	     	
		}
		else {
			cout<<" \t\t\tBox already filled! "<<"  "<<"\tPLEASE TRY AGAIN  "<<endl;
			player_turn();
		}
	
		display_board();
	}
	
	// Implementations of virtual functions 
	virtual bool gameover(){
	
		// 3 scenorio for gameover 
		//check win
		for( int i = 0 ; i<3 ; i++)
		if(board[i][0] == board[i][1] && board[i][0] == board[i][2]  || board[0][i] == board[1][i] && board[0][i] == board[2][i])    // row and column 
		return false ;
		
		//for digonal 
		if( board[0][0] == board[1][1] && board[0][0] == board[2][2] ||  board[0][2] == board[1][1] && board[0][2] == board[2][0] )
		return false;
		
		//continue or over game 
		for(int i = 0 ; i< 3 ; i++)
		for( int j = 0 ; j<3; j++)
		 if(board[i][j ] != 'X' && board[i][j] != '0')
		  return true;
		  
		//game draw 
		draw = true;
		return false;
	}
};


int main() {
	
	// TicTacToe p; we cannot create an instance of abstract class 
	
	TicTacToe *p;
	Player o;
	
	// run time polymorphism
	p = &o;
	
	// Room1 r1;
	// Room1 r2;
	// Room1 r3;
	
	// rum time polymorphism 
	//	p = &r1;
	//	p = &r2;
	//	p = &r3;
	
	// oppostie at first it will return false 
	// so 0 we use ! not it's confusion so in gameover for win we return false and continue true
	while( p -> gameover() ){  
         
		p -> display_board();
    	p -> player_turn();
    	p -> gameover();
    	
    }
     
    if( p->turn == 'X' &&  p->draw == false)
		cout<<"\tPlayer2 [0] wins!! Congratulation "<<endl ;
		
 	else if( p->turn == '0' && p->draw == false)
		cout<<"\tPlayer1 [X]  wins!! Congratulation "<<endl ;
		
	else
		cout<<"Game draw  !!"<<endl;
     
	return 0 ;
}

