# Balaji.java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.Stage;
import java.util.ArrayList;

class Book {
    String title;
    double price;
    int quantity;
    Book(String title, double price, int quantity) {
        this.title = title;
        this.price = price;
        this.quantity = quantity;
    }
}

public class BookstorePOS extends Application {
    ArrayList<Book> books = new ArrayList<>();
    TextArea output = new TextArea();

    @Override
    public void start(Stage stage) {
        TextField titleField = new TextField();
        TextField priceField = new TextField();
        TextField qtyField = new TextField();
        Button addBtn = new Button("Add Book");
        Button showBtn = new Button("Show Inventory");

        addBtn.setOnAction(e -> {
            String t = titleField.getText();
            double p = Double.parseDouble(priceField.getText());
            int q = Integer.parseInt(qtyField.getText());
            books.add(new Book(t, p, q));
            output.appendText("Book Added: " + t + "\n");
        });

        showBtn.setOnAction(e -> {
            output.clear();
            for (Book b : books)
                output.appendText(b.title + " - Rs." + b.price + " (" + b.quantity + ")\n");
        });

        VBox root = new VBox(10, new Label("Title:"), titleField,
                new Label("Price:"), priceField, new Label("Quantity:"), qtyField,
                addBtn, showBtn, output);

        stage.setScene(new Scene(root, 400, 400));
        stage.setTitle("Bookstore Inventory and POS System");
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
