package jump61;

import ucb.gui.TopLevel;
import ucb.gui.LayoutSpec;

import java.io.PrintWriter;
import java.io.Writer;

import java.util.Observable;
import java.util.Observer;

import static jump61.Side.*;

/** The GUI controller for jump61.  To require minimal change to textual
 *  interface, we adopt the strategy of converting GUI input (mouse clicks)
 *  into textual commands that are sent to the Game object through a
 *  a Writer.  The Game object need never know where its input is coming from.
 *  A Display is an Observer of Games and Boards so that it is notified when
 *  either changes.
 *  @author Ruhao Xia
 */
class Display extends TopLevel implements Observer {

    /** A new window with given TITLE displaying GAME, and using COMMANDWRITER
     *  to send commands to the current game. */
    Display(String title, Game game, Writer commandWriter) {
        super(title, true);
        _game = game;
        _board = game.getBoard();
        _commandOut = new PrintWriter(commandWriter);
        _boardWidget = new BoardWidget(game, _commandOut);
        add(_boardWidget, new LayoutSpec("y", 1, "width", 2));
        addMenuButton("Game->New Game", "newGame");
        addMenuButton("Game->Quit", "quit");
        addMenuRadioButton("Options->Red Manual", "Red", true, "manualRed");
        addMenuRadioButton("Options->Red AI", "Red", false, "autoRed");
        addMenuRadioButton("Options->Blue Manual", "Blue", false, "manualBlue");
        addMenuRadioButton("Options->Blue AI", "Blue", true, "autoBlue");
        addMenuButton("Options->Set Seed", "seed");
        addMenuButton("Options->Board Size", "size");
        _board.addObserver(this);
        _game.addObserver(this);
        display(true);
    }

    /** Response to "Quit" button click. */
    void quit(String dummy) {
        System.exit(0);
    }

    /** Start the game. */
    void newGame(String dummy) {
        _commandOut.println("clear");
        _commandOut.println("start");
    }

    /** Set PLAYER to. */
    void autoRed(String dummy) {
        _commandOut.println("auto red");
    }
    /** Set PLAYER to. */
    void autoBlue(String dummy) {
        _commandOut.println("auto blue");
    }
    /** Set PLAYER to. */
    void manualRed(String dummy) {
        _commandOut.println("manual red");
    }
    /** Set PLAYER to. */
    void manualBlue(String dummy) {
        _commandOut.println("manual blue");
    }
    /** Set SEED. */
    void seed(String dummy) {
        String num = getTextInput("Enter seed value",
                "SEED", "question", "0");
        int inte = Integer.parseInt(num);
        _commandOut.printf("seed" + inte + "\n");
    }
    /** Set SIZE. */
    void size(String dummy) {
        String num = getTextInput("Enter new board size (2-20)",
                "Board Size", "question", "6");
        int inte = Integer.parseInt(num);
        _commandOut.printf("size " + inte + "\n");
    }

    /** Update the Board for OBS and OBJ. */
    @Override
    public void update(Observable obs, Object obj) {
        _boardWidget.update();
        frame.pack();
        _boardWidget.repaint();
    }

    /** The current game that I am controlling. */
    private Game _game;
    /** The board maintained by _game (readonly). */
    private Board _board;
    /** The widget that displays the actual playing board. */
    private BoardWidget _boardWidget;
    /** Writer that sends commands to our game. */
    private PrintWriter _commandOut;
}
