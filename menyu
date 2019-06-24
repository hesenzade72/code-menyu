import com.mysql.fabric.jdbc.FabricMySQLDriver;

import java.sql.*;

/**
 * Table "menu in the restaurant." Columns: the name of the dish,
 * its cost, weight, the presence of discounts. Write code to add
 * records to the table and the sample according to the criteria
 * "cost from-to", "only with a discount" to select a set of dishes
 * so that their total weight is no more than 1 kg.
 * Created by user on 12.07.2015.
 */
public class Main {
    private static final String URL = "jdbc:mysql://localhost/mydb";
    private static final String USERNAME = "root";
    private static final String PASSWORD = "root";

    private static final String CREATE_TABLE_SQL = "CREATE TABLE IF NOT EXISTS mydb.cartDuJour (" +
            "id_dish INT NOT NULL AUTO_INCREMENT PRIMARY KEY," +
            "nameOfDish VARCHAR(50) NULL," +
            "cost INT(5) NULL," +
            "weight INT(3) NULL," +
            "discounts FLOAT(2) NULL)";

    private static final String QUERY_COST_FROM_TO = "SELECT * FROM cartdujour WHERE cost > 10 AND cost < 20";
    private static final String QUERY_ONLY_WITH_DISCOUNT = "SELECT * FROM cartdujour WHERE discounts IS NOT NULL";
    private static final String QUERY_TOTAL_WEIGHT = "SELECT * FROM cartdujour WHERE weight < 1000";



    public static void main(String[] args) {
        try {
            Driver driver = new FabricMySQLDriver();
            DriverManager.registerDriver(driver);
        } catch (SQLException e) {
            System.err.println("Не удалось загрузить класс драйвера!");
        }

        try (Connection connection = DriverManager.getConnection(URL,USERNAME,PASSWORD);
             Statement statement = connection.createStatement()){
            // Создание таблицы
            statement.execute(CREATE_TABLE_SQL);

            // Выполнение запроса
            //ResultSet resultSet = statement.executeQuery(QUERY_COST_FROM_TO);
            //ResultSet resultSet = statement.executeQuery(QUERY_ONLY_WITH_DISCOUNT);
            ResultSet resultSet = statement.executeQuery(QUERY_TOTAL_WEIGHT);

            if (resultSet.next()){
                while (resultSet.next()){
                    int id_dish = resultSet.getInt("id_dish");
                    String nameOfDish = resultSet.getString("nameOfDish");
                    int cost = resultSet.getInt("cost");
                    int weight = resultSet.getInt("weight");
                    float discounts = resultSet.getFloat("discounts");

                    System.out.println("ID Блюда: " + id_dish + "\t" +
                            "Название блюда: " +  nameOfDish + "\t" +
                            "Цена: " + cost + "\t" +
                            "Вес: " + weight + "\t" +
                            "Скидка: " + discounts);
                }
            }else {
                System.err.println("Данных удовлетворяющих запросу не найдено!");
            }

        }catch (SQLException e){
            e.printStackTrace();
        }


    }
}
