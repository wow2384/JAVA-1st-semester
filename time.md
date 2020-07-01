# JAVA-1st-semester
```
package engine.swing.chat;

import java.awt.Font;

import java.util.Calendar;

import javax.swing.JFrame;

import javax.swing.JLabel;



public class ClockEx extends JFrame{

	JLabel timeLbl = new JLabel();

	Font fnt = new Font("Serif", Font.BOLD, 100);

	public ClockEx(){

		add(timeLbl, "Center");

		timeLbl.setFont(fnt);

		setTime();

		pack();

		setVisible(true);

		

		while(true){

			try{

				Thread.sleep(1000);

			}catch(Exception e){}

			setTime();

		}

	}

	public void setTime(){

		Calendar cal = Calendar.getInstance();

		int hour = cal.get(Calendar.HOUR_OF_DAY);

		int minute = cal.get(Calendar.MINUTE);

		int second = cal.get(Calendar.SECOND);

		

		String timeStr = "";

		if(hour<10){

			timeStr="0"+hour+":";

		}else{

			timeStr=hour+":";

		}

		if(minute<10){

			timeStr+="0"+minute+":";

		}else{

			timeStr+=minute+":";

		}

		if(second<10){

			timeStr+="0"+second;

		}else{

			timeStr+=second;

		}

		timeLbl.setText(timeStr);

	}	

	public static void main(String[] args) {

		new ClockEx();



	}

}




```
