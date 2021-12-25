# getLatestID

Data di database menggunakan format "RSP-01"

public String getLatestID() {
    int hasil = 0;

    try {
        Class.forName(MYSQL_DRIVER);
        CONN = DriverManager.getConnection(MYSQL_URL, USERNAME, PASSWORD);
        STATEMENT = CONN.createStatement();

        RS = STATEMENT.executeQuery("SELECT CAST(SUBSTRING(kode, 5, LENGTH(kode)) AS UNSIGNED) AS kode FROM `responden` ORDER BY kode");

        while (RS.next()) {
            hasil = RS.getInt("kode");
        }

        RS.close();
        STATEMENT.close();
        CONN.close();
    } catch (HeadlessException | SQLException | ClassNotFoundException e) {
        dialog.exception(e);
    }

    return "RSP-"+ String.format("%02d", hasil+1);
}
