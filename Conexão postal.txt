package br.com.pratica7;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConexaoPostgre {
  private final static String url = "jdbc:postgresql://localhost/BDlivrariaUniversitaria";
  private final static String user = "postgres";
  private final static String password = "hs@2012";
  static Connection conn = null;
  
  public static Connection connect() {
    try {
      conn = DriverManager.getConnection(url, user, password);

      if (conn != null) {
        System.out.println("Connected to the PostgreSQL server successfully.");
      } else {
        System.out.println("Failed to make connection!");      
      }
    } catch (SQLException e) {
      System.out.println(e.getMessage());
    }
    return conn;
  }

  public static void printSQLException(SQLException ex) {
    for (Throwable e : ex) {
      if (e instanceof SQLException) {
        e.printStackTrace(System.err);
        System.err.println("SQLState: " + ((SQLException) e).getSQLState());
        System.err.println("Error Code: " + ((SQLException) e).getErrorCode());
        System.err.println("Message: " + e.getMessage());
        Throwable t = ex.getCause();
        while (t != null) {
          System.out.println("Cause: " + t);
          t = t.getCause();
        }
      }
    }
  }

}