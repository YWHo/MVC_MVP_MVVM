# MVC_MVP_MVVM
Summary of MVC, MVP, MVVM code example by Eric Maxwell

## The explaination of MVC, MVP, and MVVM is at:
https://academy.realm.io/posts/eric-maxwell-mvc-mvp-and-mvvm-on-android/

## The source code is at:
https://github.com/ericmaxwell2003/ticTacToe

The coding example for MVC is at 'mvc' branch.

The coding example for MVP is at 'mvp' branch.

The coding example for MVVM is at 'mvvm' branch.

## MVC - Model, View, Controller
(https://github.com/ericmaxwell2003/ticTacToe/tree/mvc)

### Model:
	Board.java
	    restart()
	    mark()
		invoke cell.setValue()
	    getWinner()
	    clearCells()
	    isValid()
	    isOutOfBound()
	    isCellValueAlreadySet()
		invoke cell.getValue()
	    isWinningMoveByPlayer()
		invoke cell.getValue()
	    flipCurrentTurn()
	Cell.java
	    getValue()
	    setValue()
	Player.java
	    enum Player

### Controller:
	TicTacToeActivity.java
	    onCreate()
		create view
		create new Board as model
	    onCreateOptionsMenu()
	    onOptionsItemSelected()
	    onCellClicked()
		invoke model.mark()
		update view due to click
	    reset()
		hide and clear view
		invoke model.restart()

## MVP - Model, View, Presenter
(https://github.com/ericmaxwell2003/ticTacToe/tree/mvp) 

### Model: 
	Board.java
	    restart()
	    mark()
		invoke cell.setValue()
	    getWinner()
	    clearCells()
	    isValid()
	    isOutOfBounds()
	    isCellValueAlreadySet()
		invoke cell.getValue()
	    isWinningMoveByPlayer()
		invoke cell.getValue()
	    flipCurrentTurn()
	Cell.java
	    getValue()
	    setValue()
	Player.java
	    enum Player


### View:
	TicTacToeView.java (interface)
	    showWinner()
	    clearWinnerDisplay()
	    clearButtons()
	    setButtonText()
	TicTacToeActivity.java
	    onCreate()
		create view
		invoke presenter.onCreate()
	    onPause()
		invoke presenter.onPause()
	    onResume()
		invoke presenter.onResume()
	    onDestroy()
		invoke presenter.onDestroy()
	    onCreateOptionsMenu()
	    onOptionsItemSelected()
		invoke presenter.onResetSelected()
	    onCellClicked()
		invoke presenter.onButtonSelected()
	    setButtonText()
	    clearButtons()
	    showWinner()
	    clearWinnerDisplay()

### Presenter:
	Presenter.java (interface)
	    onCreate()
	    onPause()
	    onResume()
	    onDestroy()
	TicTacToePresenter.java
	    onCreate()
		create new Board as model
	    onPause()
	    onResume()
	    onDestroy()
	    onButtonSelected()
	    onResetSelected()
		hide and clear view
		invoke model.restart()

## MVVM - Model, View, ViewModel
(https://github.com/ericmaxwell2003/ticTacToe/tree/mvvm)

### Model:
	Board.java
	    restart()
	    mark()
		invoke cell.setValue()
	    valueAtCell()
		invoke cell.getValue()
	    getWinner()
	    clearCells()
	    isValid()
	    isOutOfBounds()
	    isCellValueAlreadySet()
		invoke.cell.getValue()
	    isWiningMoveByPlayer()
		invoke.cell.getValue()
	Cell.java
	    getValue()
	    setValue()
	Player.java
	    enum Player
		

### View:
	TicTacToeActivity.java
	    onCreate()
		initialise data binding on layout
		set viewModel of the data binding
		invoke viewModel.onCreate()
	    onPause()
		invoke viewModel.onPause()
	    onResume()
		invoke viewModel.onResume()
	    onDestroy()
		invoke viewModel.onDestroy()
	    onCreateOptionsMenu()
	    onOptionsItemSelected()
		invoke viewModel.onResetSelected()
		
### ViewModel:
	ViewModel.java (interface)
	    onCreate()
	    onPause()
	    onResume()
	    onDestroy()
	TicTacToeVieModel.java
	    cells as ObservableArrayMap
	    winner as ObservableField
	    onCreate()
	    onPause()
	    onResume()
	    onDestroy()
	    onResetSelected()
		invoke model.restart()
		reset winner and cells
	    onClickedCellAt()
		invoke model.mark()
		update cell display
		update winner message

### Sample from Layout file:
	tictactoe.xml
	    <Button
	        style="@style/tictactoebutton"
	        android:onClick="@{() -> viewModel.onClickedCellAt(0,0)}"
	        android:text='@{viewModel.cells["00"]}' />
	    <LinearLayout
	        android:id="@+id/winnerPlayerViewGroup"
	        android:layout_width="wrap_content"
	        android:layout_height="match_parent"
	        android:gravity="center"
	        android:orientation="vertical"
	        android:visibility="@{viewModel.winner != null ? View.VISIBLE : View.GONE}"
	        tools:visibility="visible">

	        <TextView
	            android:id="@+id/winnerPlayerLabel"
	            android:layout_width="wrap_content"
	            android:layout_height="wrap_content"
	            android:layout_margin="20dp"
	            android:textSize="40sp"
	            android:text="@{viewModel.winner}"
	            tools:text="X" />
	    </LinearLayout>
