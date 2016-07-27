# Queue app - description

JAVA was used to create this project, using NETBEANS. A GUI was developed, including the required components.

Advantages of this GUI:
- Ease of use.
- Radio buttons & textfields are cleared/reset for repetitive use.
- It can be run, closed, then opened again - details of new customers will still be saved underneath the previous ones.

Disadvantages:

- Every time a radio button is clicked, it will still be printed onto the seperate file of data until 'Submit' is clicked; so it would have to be used once and accurately.
- The customers are not numbered, but placed in order from top-bottom.
- The GUI is not linked to a browser, as a frame (JFrame) cannot be added to an applet in JAVA.
- Anonymous customers would have to click on the corresponding service and on 'Anonymous', without typing their name nor last name because by default the program automatically outputs the name and last name on the file note. They would just select between Mr, Ms, Mrs & Miss. The time will also be displayed.
- Organisations would have to type their organisation name in the 'First Name' field. There would also be a title displayed. 

Below is the code for the task:
____________________________

package queuereceptiondesk;

import java.io.File;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.BufferedWriter;
import java.io.FileNotFoundException;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Scanner;

public class QueueReceptionDesk extends JFrame {

    String details;
    String disp = " ";
    TextHandler handler1 = null;
    TextHandler handler2 = null;
    TextHandler handler3 = null;
    TextHandler handler4 = null;
    TextHandler handler5 = null;
    TextHandler handler6 = null;
    TextHandler handler7 = null;

    File outFile1;

    public QueueReceptionDesk() {
        setLayout(new GridLayout(17, 5));
        setTitle("QUEUE APP");

        setSize(420, 500);
        setLocation(200, 100);

        JLabel NewCustomer = new JLabel("New Customer");
        JLabel Services = new JLabel("Services");
        JRadioButton Housing = new JRadioButton("Housing");
        JRadioButton Benefits = new JRadioButton("Benefits");
        JRadioButton CouncilTax = new JRadioButton("Council Tax");
        JRadioButton FlyTipping = new JRadioButton("Fly-tipping");
        JRadioButton MissedBin = new JRadioButton("Missed Bin");

        ButtonGroup group = new ButtonGroup();
        group.add(Housing);
        group.add(Benefits);
        group.add(CouncilTax);
        group.add(FlyTipping);
        group.add(MissedBin);

        JButton Citizen = new JButton("Citizen");
        JButton Organization = new JButton("Organization");
        JButton Anonymous = new JButton("Anonymous");

        JLabel Title = new JLabel("Title");
        JComboBox title1 = new JComboBox(new String[]{"Mr", "Ms", "Mrs", "Miss"});
        JLabel FirstName = new JLabel("First Name");
        JTextField firstname1 = new JTextField(20);
        JLabel LastName = new JLabel("Last Name");
        JTextField lastname1 = new JTextField(20);

        JButton Submit = new JButton("Submit");

        add(NewCustomer);
        add(Services);

        add(Housing);
        add(Benefits);
        add(CouncilTax);
        add(FlyTipping);
        add(MissedBin);

        add(Citizen);
        add(Organization);
        add(Anonymous);

        add(Title);
        add(title1);
        add(FirstName);
        add(firstname1);
        add(LastName);
        add(lastname1);

        add(Submit);

        setVisible(true);

        this.outFile1 = new File("Queue.txt");

        handler1 = new TextHandler();
        firstname1.addActionListener(handler1);
        handler2 = new TextHandler();
        lastname1.addActionListener(handler2);

        Housing.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Service: Housing \t");
            }
        });

        Benefits.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Service: Benefits \t");
            }
        });
        CouncilTax.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Service: Council Tax \t");
            }
        });
        FlyTipping.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Service: Fly-tipping \t");
            }
        });
        MissedBin.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Service: Missed Bin \t");
            }
        });

        //
        Citizen.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Type: Citizen \t");
            }
        });

        Organization.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Type: Organization \t");
            }
        });

        Anonymous.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writeToFile1("Type: Anonymous \t");
            }
        });

     
        Submit.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                
                
                title1.getSelectedItem();
                String value = (String) title1.getSelectedItem();

                String str1 = firstname1.getText();
                firstname1.requestFocusInWindow();
                String str2 = lastname1.getText();
                lastname1.requestFocusInWindow();

                writeToFile1(value + " " + str1 + " " + str2 + " ");
                writeToFile1("" + new java.util.Date());
                writeToFile1("______________________________");

                firstname1.setText("");
                lastname1.setText("");
                group.clearSelection();
            }
        });

    }

    BufferedWriter out;

    public void writeToFile1(String s) {
        try {
            out = new BufferedWriter(new FileWriter("Queue.txt", true));
            out.write(s);
            out.newLine();
            out.close();
        } catch (IOException e) {
            System.out.println("There was an error" + e);

        }
    }

    public static void main(String[] args) {
        QueueReceptionDesk code = new QueueReceptionDesk();
        code.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

    }

    private class TextHandler implements ActionListener {

        public void actionPerformed(ActionEvent e) {
            disp = e.getActionCommand();
            System.out.println(disp);

        }
    }

}

