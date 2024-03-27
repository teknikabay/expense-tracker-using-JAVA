# expense-tracker-using-JAVA

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.List;

public class Expense {
    public static void main(String[] args) {
        JFrame jf = new JFrame("Expense Tracker");

        jf.setVisible(true);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setLayout(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.anchor = GridBagConstraints.WEST;
        gbc.insets = new Insets(5, 5, 5, 5);

        jf.setSize(800, 800);

        JLabel jl = new JLabel("Enter Category");
        JLabel jl1 = new JLabel("Enter Amount");

        JTextField jt = new JTextField(20);
        JTextField jt1 = new JTextField(20);

        List<String> Details = new ArrayList<>();

        gbc.gridx = 0;
        gbc.gridy = 0;
        jf.add(jl, gbc);

        gbc.gridx = 1;
        jf.add(jt, gbc);

        gbc.gridx = 0;
        gbc.gridy = 1;
        jf.add(jl1, gbc);

        gbc.gridx = 1;
        jf.add(jt1, gbc);

        JButton b1 = new JButton("Add Expense");
        b1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String category = jt.getText();
                String amountStr = jt1.getText();

                // Validate and parse amount input as an integer
                try {
                    int amount = Integer.parseInt(amountStr);
                    Details.add("Category: " + category + ", Amount: " + amount);
                    jt.setText(""); // Clear category text field
                    jt1.setText(""); // Clear amount text field
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(jf, "Please enter a valid integer amount.");
                }
            }
        });

        gbc.gridx = 0;
        gbc.gridy = 2;
        jf.add(b1, gbc);

        JButton b = new JButton("Show Catalog");
        b.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                StringBuilder sb = new StringBuilder("All Expenses\n");
                for (String expense : Details) {
                    sb.append(expense).append("\n");
                }
                JOptionPane.showMessageDialog(jf, sb.toString());
            }
        });

        gbc.gridx = 0;
        gbc.gridy = 3;
        jf.add(b, gbc);

        jf.pack();
    }
}
