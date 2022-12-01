package br.com.pratica7;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class ExcluirLivro {
  private static final String DELETE_LIVROS_BY_ID_SQL = "DELETE FROM livro WHERE id_isbn = ?";

  public int deleteRecord(String id_isbn) {    
    int result = 0;
    try {
      Connection conn = ConexaoPostgre.connect();
      PreparedStatement pstmt = conn.prepareStatement(DELETE_LIVROS_BY_ID_SQL);
      pstmt.setString(1, id_isbn);
      result = pstmt.executeUpdate();
    } catch (SQLException e) {
      ConexaoPostgre.printSQLException(e);
    }
    return result;
  }
}