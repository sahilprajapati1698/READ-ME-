Sahil Prajapati 

CSC 7200 

Student ID - @01410508 

Question 1 Answer Code 


import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.scene.paint.Color;
import javafx.stage.Stage;

public class SimpleCalculator extends Application {

    private TextField number1Field;
    private TextField number2Field;
    private TextField resultField;

    @Override
    public void start(Stage primaryStage) {
        // Step 2: Create the GUI layout
        GridPane gridPane = new GridPane();
        gridPane.setHgap(10);
        gridPane.setVgap(10);
        gridPane.setPadding(new Insets(20));

        Label number1Label = new Label("Number 1:");
        Label number2Label = new Label("Number 2:");
        Label resultLabel = new Label("Result:");

        number1Field = new TextField();
        number2Field = new TextField();
        resultField = new TextField();
        resultField.setEditable(false);

        Button addButton = new Button("Add");
        Button subtractButton = new Button("Subtract");
        Button multiplyButton = new Button("Multiply");
        Button divideButton = new Button("Divide");
        Button remainderButton = new Button("Remainder");

        // Step 3: Implement event handling for the buttons
        addButton.setOnAction(e -> performOperation((a, b) -> a + b));
        subtractButton.setOnAction(e -> performOperation((a, b) -> a - b));
        multiplyButton.setOnAction(e -> performOperation((a, b) -> a * b));
        divideButton.setOnAction(e -> performOperation((a, b) -> a / b));
        remainderButton.setOnAction(e -> performOperation((a, b) -> a % b));

        // Step 4: Set alignment, title, and background color
        gridPane.setAlignment(javafx.geometry.Pos.CENTER);
        gridPane.setStyle("-fx-background-color: #F0F0F0;");
        primaryStage.setTitle("Simple Calculator");

        // Add components to the grid pane
        gridPane.add(number1Label, 0, 0);
        gridPane.add(number1Field, 1, 0);
        gridPane.add(number2Label, 0, 1);
        gridPane.add(number2Field, 1, 1);
        gridPane.add(resultLabel, 0, 2);
        gridPane.add(resultField, 1, 2);
        gridPane.add(addButton, 0, 3);
        gridPane.add(subtractButton, 1, 3);
        gridPane.add(multiplyButton, 0, 4);
        gridPane.add(divideButton, 1, 4);
        gridPane.add(remainderButton, 0, 5);

        // Set up the scene and show the stage
        Scene scene = new Scene(gridPane, 300, 250);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void performOperation(MathOperation operation) {
        try {
            double number1 = Double.parseDouble(number1Field.getText());
            double number2 = Double.parseDouble(number2Field.getText());
            double result = operation.calculate(number1, number2);
            resultField.setText(Double.toString(result));
        } catch (NumberFormatException e) {
            resultField.setText("Error");
        }
    }

    @FunctionalInterface
    private interface MathOperation {
        double calculate(double a, double b);
    }

    public static void main(String[] args) {
        launch(args);
    }
}


