import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleCalculator extends JFrame implements ActionListener {
    private JTextField inputField;
    private JButton[] numberButtons;
    private JButton addButton, subButton, mulButton, divButton, equalButton, clearButton;
    private String operator;
    private double num1, num2, result;

    public SimpleCalculator() {
        // Create the frame
        setTitle("Simple Calculator");
        setSize(400, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Create input field
        inputField = new JTextField();
        inputField.setFont(new Font("Arial", Font.PLAIN, 24));
        inputField.setEditable(false);
        add(inputField, BorderLayout.NORTH);

        // Create buttons
        JPanel buttonPanel = new JPanel();
        buttonPanel.setLayout(new GridLayout(4, 4, 10, 10));

        numberButtons = new JButton[10];
        for (int i = 0; i < 10; i++) {
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            buttonPanel.add(numberButtons[i]);
        }

        addButton = new JButton("+");
        subButton = new JButton("-");
        mulButton = new JButton("*");
        divButton = new JButton("/");
        equalButton = new JButton("=");
        clearButton = new JButton("C");

        addButton.addActionListener(this);
        subButton.addActionListener(this);
        mulButton.addActionListener(this);
        divButton.addActionListener(this);
        equalButton.addActionListener(this);
        clearButton.addActionListener(this);

        buttonPanel.add(addButton);
        buttonPanel.add(subButton);
        buttonPanel.add(mulButton);
        buttonPanel.add(divButton);
        buttonPanel.add(equalButton);
        buttonPanel.add(clearButton);

        add(buttonPanel, BorderLayout.CENTER);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        for (int i = 0; i < 10; i++) {
            if (e.getSource() == numberButtons[i]) {
                inputField.setText(inputField.getText() + i);
            }
        }

        if (e.getSource() == addButton) {
            num1 = Double.parseDouble(inputField.getText());
            operator = "+";
            inputField.setText("");
        } else if (e.getSource() == subButton) {
            num1 = Double.parseDouble(inputField.getText());
            operator = "-";
            inputField.setText("");
        } else if (e.getSource() == mulButton) {
            num1 = Double.parseDouble(inputField.getText());
            operator = "*";
            inputField.setText("");
        } else if (e.getSource() == divButton) {
            num1 = Double.parseDouble(inputField.getText());
            operator = "/";
            inputField.setText("");
        } else if (e.getSource() == equalButton) {
            num2 = Double.parseDouble(inputField.getText());
            switch (operator) {
                case "+":
                    result = num1 + num2;
                    break;
                case "-":
                    result = num1 - num2;
                    break;
                case "*":
                    result = num1 * num2;
                    break;
                case "/":
                    if (num2 != 0) {
                        result = num1 / num2;
                    } else {
                        JOptionPane.showMessageDialog(this, "Error: Division by zero is not allowed.");
                        return;
                    }
                    break;
            }
            inputField.setText(String.valueOf(result));
        } else if (e.getSource() == clearButton) {
            inputField.setText("");
            num1 = num2 = result = 0;
            operator = "";
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            SimpleCalculator calculator = new SimpleCalculator();
            calculator.setVisible(true);
        });
    }
}# Calculator_Java
