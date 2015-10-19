package snake;
 
    import javax.swing.*;
    import java.awt.*;
    import java.awt.event.*;
 
 
public class MainFrame{
        public static void main(String args[]){
            SnakeFrame frame = new SnakeFrame();
                
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
                
 
        }
    }
     
    class SnakeFrame extends JFrame {
 
    private static class NewMenuListener implements ActionListener {
        public NewMenuListener() {
        }
        @Override
        public void actionPerformed(ActionEvent e) {
            throw new UnsupportedOperationException("Not supported yet.");
        }
    }
            int i = 0;
            SnakePanel panel;
            boolean live = true;
            SnakeBody snake = new SnakeBody();
            SnakeDirection direction = new SnakeDirection(0);
            public food f = new food();
            public static  boolean eaten = false;
            public boolean alive = true;
            public boolean done = true;
private JMenuBar menu = null;
private final String fileItems[] = new String []{"Новая игра", "Выход"};
 
                
              
                
                
     
        public  SnakeFrame(){
            setSize(500,300);
            setTitle("Змейка");
createMenu();
setJMenuBar(menu);
 
            panel = new SnakePanel();
            panel.setBackground(new Color(10, 10, 10));
            add(panel);
     
        }
        public static boolean getEaten(){
            return eaten;
        }
        public static void setEaten(boolean eat){
            eaten = eat;
        }
        //Second Thread
       class SnakeThread implements Runnable{
            Graphics g=null;
     
            public SnakeThread(){
                Thread t;
                t = new Thread(this);
                System.out.println("Second thread");
                t.start();
            }
     
            public void run(){
                System.out.println("Внутри run");
            while(alive == true){
     
                try {
     
                    Thread.sleep(200);
                 //System.out.println("Inside try"+i);
     
                }
                catch (InterruptedException e) {
                            // Do nothing
                }
     
                  snake.move(direction);
                  eat();
                  die();
                  panel.repaint();
                 done = true;
     
            }
     
            }
     
        }
     
        class SnakePanel extends JPanel  {
     
            public SnakePanel(){
              new SnakeThread();
              KeyHendler listener =  new KeyHendler();
              addKeyListener(listener);
              setFocusable(true);
     
            }
            public void paintComponent(Graphics g){
                //super.paintComponent(g);
                g.clearRect(0,0,500,300);
                snake.paint(g);
     
     
                if(eaten == true)
                   f.changePosition();
                f.paintFood(g);
     
            }
     
        }
     
        public void die(){
        if(snake.body.getLast().x >47 || snake.body.getLast().x <0 ||
                    snake.body.getLast().y >25 ||snake.body.getLast().y <0 )
            alive = false;
            for(int i =1;i<snake.body.size()-1;i++){
     
                if(snake.body.getLast().x ==snake.body.get(i).x && snake.body.getLast().y ==snake.body.get(i).y){
                   System.out.println(i);
                    alive = false;
                }
     
            }
        }
         public void eat(){
             //f = SnakeFrame.;
             if(f.foodx == snake.body.getLast().x && f.foody == snake.body.getLast().y){
                 Point p = new Point (f.foodx,f.foody);
                 System.out.println("Coordinats equals");
                 //int numberOfParts = body.size();
                 snake.body.add(0,p);
                 eaten = true;
                 //fod.changePosition();
     
             }
         }
     
        private class KeyHendler implements KeyListener{
            public void keyPressed(KeyEvent event){
     
                int keyCode = event.getKeyCode();
     
                if(keyCode == KeyEvent.VK_RIGHT&&done == true){ direction.changeToRight();done = false;}
                if(keyCode == KeyEvent.VK_LEFT&&done == true){ direction.changeToLeft();done = false;}
                if(keyCode == KeyEvent.VK_UP&&done == true){ direction.changeToUp();done = false;}
                if(keyCode == KeyEvent.VK_DOWN&&done == true) {direction.changeToDown();done = false;}
     
            }
            public void keyReleased(KeyEvent event){
                }
            public void keyTyped(KeyEvent event){
     
            }        
        }
     
        public class SnakeDirection{      
                public final  int right = 0;
            public final  int down = 1;
            public final  int left = 2;
            public final  int up = 3;
     
            public int state = 0;
     
            public SnakeDirection(int s ){
                state =s;
            }
     
            public void changeToRight(){
                    if(state != left)
                state = right;
            }
            public void changeToLeft(){
                if(state != right)
                state = left;
            }
            public void changeToUp(){
                if(state != down)
                state = up;
            }
            public void changeToDown(){
                if(state != up)
                state = down;
            }
        }
            
            private void createMenu() {
menu = new JMenuBar();
JMenu fileMenu = new JMenu("Игра");
for (int i = 0; i < fileItems.length; i++) {
JMenuItem item = new JMenuItem(fileItems[i]);
item.setActionCommand(fileItems[i].toLowerCase());
item.addActionListener(new NewMenuListener());
fileMenu.add(item);
}
fileMenu.insertSeparator(1);
 
menu.add(fileMenu);
    }
        }
        
        package snake;
 
    import javax.swing.*;
    import java.awt.*;
    import java.awt.event.*;
 
 
public class MainFrame{
        public static void main(String args[]){
            SnakeFrame frame = new SnakeFrame();
                
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
                
 
        }
    }
     
    class SnakeFrame extends JFrame {
 
    private static class NewMenuListener implements ActionListener {
        public NewMenuListener() {
        }
        @Override
        public void actionPerformed(ActionEvent e) {
            throw new UnsupportedOperationException("Not supported yet.");
        }
    }
            int i = 0;
            SnakePanel panel;
            boolean live = true;
            SnakeBody snake = new SnakeBody();
            SnakeDirection direction = new SnakeDirection(0);
            public food f = new food();
            public static  boolean eaten = false;
            public boolean alive = true;
            public boolean done = true;
private JMenuBar menu = null;
private final String fileItems[] = new String []{"Новая игра", "Выход"};
 
                
              
                
                
     
        public  SnakeFrame(){
            setSize(500,300);
            setTitle("Змейка");
createMenu();
setJMenuBar(menu);
 
            panel = new SnakePanel();
            panel.setBackground(new Color(10, 10, 10));
            add(panel);
     
        }
        public static boolean getEaten(){
            return eaten;
        }
        public static void setEaten(boolean eat){
            eaten = eat;
        }
        //Second Thread
       class SnakeThread implements Runnable{
            Graphics g=null;
     
            public SnakeThread(){
                Thread t;
                t = new Thread(this);
                System.out.println("Second thread");
                t.start();
            }
     
            public void run(){
                System.out.println("Внутри run");
            while(alive == true){
     
                try {
     
                    Thread.sleep(200);
                 //System.out.println("Inside try"+i);
     
                }
                catch (InterruptedException e) {
                            // Do nothing
                }
     
                  snake.move(direction);
                  eat();
                  die();
                  panel.repaint();
                 done = true;
     
            }
     
            }
     
        }
     
        class SnakePanel extends JPanel  {
     
            public SnakePanel(){
              new SnakeThread();
              KeyHendler listener =  new KeyHendler();
              addKeyListener(listener);
              setFocusable(true);
     
            }
            public void paintComponent(Graphics g){
                //super.paintComponent(g);
                g.clearRect(0,0,500,300);
                snake.paint(g);
     
     
                if(eaten == true)
                   f.changePosition();
                f.paintFood(g);
     
            }
     
        }
     
        public void die(){
        if(snake.body.getLast().x >47 || snake.body.getLast().x <0 ||
                    snake.body.getLast().y >25 ||snake.body.getLast().y <0 )
            alive = false;
            for(int i =1;i<snake.body.size()-1;i++){
     
                if(snake.body.getLast().x ==snake.body.get(i).x && snake.body.getLast().y ==snake.body.get(i).y){
                   System.out.println(i);
                    alive = false;
                }
     
            }
        }
         public void eat(){
             //f = SnakeFrame.;
             if(f.foodx == snake.body.getLast().x && f.foody == snake.body.getLast().y){
                 Point p = new Point (f.foodx,f.foody);
                 System.out.println("Coordinats equals");
                 //int numberOfParts = body.size();
                 snake.body.add(0,p);
                 eaten = true;
                 //fod.changePosition();
     
             }
         }
     
        private class KeyHendler implements KeyListener{
            public void keyPressed(KeyEvent event){
     
                int keyCode = event.getKeyCode();
     
                if(keyCode == KeyEvent.VK_RIGHT&&done == true){ direction.changeToRight();done = false;}
                if(keyCode == KeyEvent.VK_LEFT&&done == true){ direction.changeToLeft();done = false;}
                if(keyCode == KeyEvent.VK_UP&&done == true){ direction.changeToUp();done = false;}
                if(keyCode == KeyEvent.VK_DOWN&&done == true) {direction.changeToDown();done = false;}
     
            }
            public void keyReleased(KeyEvent event){
                }
            public void keyTyped(KeyEvent event){
     
            }        
        }
     
        public class SnakeDirection{      
                public final  int right = 0;
            public final  int down = 1;
            public final  int left = 2;
            public final  int up = 3;
     
            public int state = 0;
     
            public SnakeDirection(int s ){
                state =s;
            }
     
            public void changeToRight(){
                    if(state != left)
                state = right;
            }
            public void changeToLeft(){
                if(state != right)
                state = left;
            }
            public void changeToUp(){
                if(state != down)
                state = up;
            }
            public void changeToDown(){
                if(state != up)
                state = down;
            }
        }
            
            private void createMenu() {
menu = new JMenuBar();
JMenu fileMenu = new JMenu("Игра");
for (int i = 0; i < fileItems.length; i++) {
JMenuItem item = new JMenuItem(fileItems[i]);
item.setActionCommand(fileItems[i].toLowerCase());
item.addActionListener(new NewMenuListener());
fileMenu.add(item);
}
fileMenu.insertSeparator(1);
 
menu.add(fileMenu);
    }
        }
        
        
        
  package snake;
 
    import java.util.LinkedList;
    import java.util.ListIterator;
    import java.awt.*;
 
    public class SnakeBody extends Object {
        //List witch contains snake body;
         LinkedList<Point> body  = new LinkedList<Point>();
            //part of snake
            final int size = 10;
            //co-ordinate X of one body part
            public int x;
            //co-ordinate Y of one body part
            public int y;
     
            food fod ;
     
     
     
    //  constructor that initialize snake boby
        SnakeBody(){
            Point point;
     
            point = new Point(3,6);  body.add(0,point);
            point = new Point(4,6);  body.add(1,point);
            point = new Point(5,6);  body.add(2,point);
            point = new Point(6,6);  body.add(3,point);
            point = new Point(7,6);  body.add(4,point);
        }
     
         public void paint(Graphics g){
            for(int i =0; i<body.size();i++){
                 Point p = body.get(i);
                 int bodyx =(int) p.getX();
                 int bodyy =(int) p.getY();
                 //g.drawString("zzzzzzzz",100,100);
                 g.setColor(new Color(22,26,218));
                 g.fillRect(bodyx*size,bodyy*size,size,size);
                }
         }
     
         public void move(SnakeFrame.SnakeDirection d){
            LinkedList<Point> bodyCopy  = new LinkedList<Point>();
             copyList(bodyCopy,body);
             ListIterator it = body.listIterator();
             int iter = body.size();
     
             for(int i = iter-1; i >=0;i--) {
                 Point p = body.get(i);
     
                 if(body.get(i) == body.getLast()){
                     if(d.state == d.right )
                        p.x = p.x +1;
                     else if(d.state == d.down)
                        p.y = p.y +1;
                     else if(d.state == d.up)
                        p.y = p.y -1;
                     else if(d.state == d.left)
                        p.x = p.x -1;                 
                 }
                 else  {
     
                     Point p1 = bodyCopy.get(i+1);
     
                     p.x = p1.x;
                     p.y = p1.y;
                 }
             }
     
         }
    
         public void copyList(LinkedList a, LinkedList b){
            for(int i =0;i< b.size();i++)
            {
                Point p =(Point) b.get(i) ;
                a.add(p.clone());
            }
         }
 
     
     
    }
