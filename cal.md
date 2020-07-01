# JAVA-1st-semester

```
package home;

import java.awt.BorderLayout;
import java.awt.GridLayout;
import java.awt.Panel;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;


public class Calculator extends JFrame{
	private JButton[] buttons;
	private String[] labels = {
			"1", "2", "3" , "4", "5", "6", "7", "8", "9", 
			"+", "-", "*", "/", "C", "="};
	private JLabel screen;
	int t1,t3,sum; 
	String t2; 

	public Calculator(){
		screen = new JLabel();
		setSize(400,150);
		setTitle("Calculator"); 
		int index =0;
		buttons =new JButton[15];
		Panel panel = new Panel();
		screen.setText("0.");

		panel.setLayout(new GridLayout(0,4)); 
		for(int rows= 0; rows <15; rows++) {
				buttons[index] =new JButton(labels[index]);
				panel.add(buttons[index]);
				index++;
			}
		for(int num=0; num<9; num++) { 
			int i1=num;
			buttons[num].addActionListener(e->{
				screen.setText(labels[i1]);
			});
		}
		for(int num=9; num<13; num++) { 
			int i2=num;
			buttons[num].addActionListener(e->{
				t1=Integer.parseInt(screen.getText());
				screen.setText(labels[i2]);
				t2=labels[i2];
			});
		}
		buttons[13].addActionListener(e->{ 
			t1=0;
			t2="";
			screen.setText("0.");
		});
		buttons[14].addActionListener(e->{
			t3 = Integer.parseInt(screen.getText()); 
			if(t2=="+") {
				sum = t1+t3;
				screen.setText(Integer.toString(sum));
				t1=t3=0;
			}
			else if(t2=="-") {
				sum = t1-t3;
				screen.setText(Integer.toString(sum));
				t1=t3=0;
			}
			else if(t2 == "*") {
				sum = t1*t3;
				screen.setText(Integer.toString(sum));
				t1=t3=0;
			}
			else if(t2 == "/") {
				sum = t1/t3;
				screen.setText(Integer.toString(sum));
				t1=t3=0;
			}
		});
		add(screen,BorderLayout.NORTH);
		add(panel,BorderLayout.CENTER);
		setVisible(true);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);		
		
	}
	public static void main(String[] args) {
		Calculator i = new Calculator();
		
	}
}

```
