# Aprogramiranje
----------------------------------------------------------A01-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dTable = new DataTable();
    string connectionString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A01_Biblioteka_Baza.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(connectionString))
    {
        using (SqlDataAdapter dAdapter = new SqlDataAdapter(upit, konekcija))
        {
            dAdapter.Fill(dTable);
        }
    }
    return dTable;
}

public static int IzvrsiNeUpit(string neUpit)
{
    int afektovano;
    string connectionString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A01_Biblioteka_Baza.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(connectionString))
    {
        using (SqlCommand komanda = new SqlCommand(neUpit, konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
private void RefreshListView()
{
    listView1.Items.Clear();

    string upit1 = "select CitalacID, MaticniBroj, Ime, Prezime, Adresa from Citalac";
    DataTable dt = Baza.IzvrsiUpit(upit1);

    foreach (DataRow red in dt.Rows)
    {
        string[] podaci = { red[0].ToString(), red[1].ToString(), red[2].ToString(), red[3].ToString(), red[4].ToString() };
        ListViewItem stavka = new ListViewItem(podaci);
        listView1.Items.Add(stavka);
    }

    //tab2 inicijalizacija comboBoxa

    string upit2 = "select CitalacId as sifra,str(CitalacId)+ ' ' +Ime +' '+Prezime as ime from Citalac";
    cmbCitalac.DataSource = Baza.IzvrsiUpit(upit2);
    cmbCitalac.ValueMember = "sifra";
    cmbCitalac.DisplayMember = "ime";
}

private void Form1_Load(object sender, EventArgs e)
{

    this.RefreshListView();
    listView1.MultiSelect = false;
    listView1.FullRowSelect = true;
}
----------------------------------------------------------A02-Baza.cs-
------------------------------------------------Upis u list view/box/combobox
----------------------------------------------------------A03-Baza.cs-
public static DataTable IzvrsiUpit (string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\EvidencijaRadnika.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit, konekcija))
        {
            da.Fill(dt);
        }
    }

    return dt;
}


public static int IzvrsiNeUpit (string neupit)
{
    int afektovano;

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\EvidencijaRadnika.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda = new SqlCommand(neupit,konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
private void RefreshListView()
{
    listView1.Items.Clear();

    string upit = $@"select ProjekatId, Naziv, 
                    FORMAT(DatumPocetka,'dd.MM.yyyy'), 
                    Budzet, 
                    ProjekatZavrsen, Opis from Projekat";

    DataTable dt = Baza.IzvrsiUpit(upit);

    foreach(DataRow red in dt.Rows)
    {
        string[] podaci = {
                            red[0].ToString(),
                            red[1].ToString(),
                            red[2].ToString(),
                            red[3].ToString(),
                            red[4].ToString(),
                            red[5].ToString()
                          };

        ListViewItem stavka = new ListViewItem(podaci);
        listView1.Items.Add(stavka);
    }
}

private void Form1_Load(object sender, EventArgs e)
{
    RefreshListView();
    //listView1.FullRowSelect = true;
    //listView1.MultiSelect = false;
}
----------------------------------------------------------A04-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A04_SeoskiTurizam_Baza.mdf;Integrated Security=True";
   

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit, konekcija))
        {
            da.Fill(dt);
        }
    }

    return dt;
}

public static int IzvrsiNeupit(string neUpit)

{
    int afektovano = 0;
    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A04_SeoskiTurizam_Baza.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda = new SqlCommand(neUpit, konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
public void UcitavanjePodataka()
{
    listView1.Items.Clear();

    string upit = "SELECT s.seloID, s.Naziv, g.grad FROM Selo s, Grad g " +
        "WHERE s.gradID = g.gradID";

    try
    {
        DataTable dt = Baza.IzvrsiUpit(upit);
        foreach (DataRow dr in dt.Rows)
        {
            string[] podaci =
            {
                dr[0].ToString(),
                dr[1].ToString(),
                dr[2].ToString(),
            };
            ListViewItem item = new ListViewItem(podaci);
            listView1.Items.Add(item);
        }
    }
    catch (Exception ex) 
    {
        MessageBox.Show("Neuspešno učitavanje podataka", "Info", MessageBoxButtons.OK, MessageBoxIcon.Error);
    }
}
----------------------------------------------------------A05-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Baza_A05_ProduzeniBoravak.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit,konekcija))
        {
            da.Fill(dt);
        }
    }
        return dt;
}

public static int IzvrsiNeupit(string neUpit)
{
    int afektovano = 0;
    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Baza_A05_ProduzeniBoravak.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda = new SqlCommand(neUpit,konekcija))
        {
            konekcija.Open();
            afektovano=komanda.ExecuteNonQuery();
            konekcija.Close();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
public void RefreshListView()
{
    listView1.Items.Clear();

    string upit = "SELECT AktivnostiID, NazivAktivnosti, Dan, " +
        "Pocetak, Zavrsetak " +
        "FROM Aktivnosti";
   
    DataTable dt = Baza.IzvrsiUpit(upit);

    foreach (DataRow red in dt.Rows) 
    {
        string[] podaci =
        {
            red[0].ToString(),
            red[1].ToString(),
            red[2].ToString(),
            Convert.ToDateTime(red[3].ToString()).ToString("HH:mm"),
            Convert.ToDateTime(red[4].ToString()).ToString("HH:mm")
        };
        ListViewItem stavka = new ListViewItem(podaci);
        listView1.Items.Add(stavka);
    }
}

private void Form1_Load(object sender, EventArgs e)
{
    RefreshListView();
    listView1.MultiSelect = false;
    listView1.FullRowSelect = true;
}
----------------------------------------------------------A06-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\BazaA06_PolovniAutomobili.mdf;Integrated Security=True";

    using(SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit, konekcija))
        {
            da.Fill(dt);
        }
    }
    return dt;
}

public static int IzvrsiNeupit(string neUpit)
{
    int afektovano;

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\BazaA06_PolovniAutomobili.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda = new SqlCommand(neUpit,konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
            konekcija.Close();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
public void PopuniListBox()
{
        string upit = @"select m.ModelID as id,FORMAT(m.ModelID,'D3')+' '+
                p.Naziv+ ', '+m.Naziv  as nazivModela " +
        "from Model as m left join Proizvodjac as p " +
        "on m.ProizvodjacID=p.ProizvodjacID ";
        

    DataTable dt = Baza.IzvrsiUpit(upit);

    listBox1.DataSource = dt;
    listBox1.ValueMember = "id";
    listBox1.DisplayMember = "nazivModela";

    listBox1.SelectedItems.Clear();
}
 public void PopuniComboBox()
{
    string upit = "select ProizvodjacID as id, Naziv as nazivProizvodjaca " +
        "from Proizvodjac";

    DataTable dt = Baza.IzvrsiUpit(upit);
    cmbProizvodjac.DataSource = dt;
    cmbProizvodjac.ValueMember = "id";
    cmbProizvodjac.DisplayMember = "nazivProizvodjaca";

    
}
private void Form1_Load(object sender, EventArgs e)
{
    PopuniListBox();
    PopuniComboBox();
}
----------------------------------------------------------A10-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A10RibolovackoDrustvo_Baza.mdf;Integrated Security=True";
    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit,konekcija))
        {
            da.Fill(dt);
        }
    }
    return dt;
}

public static int IzvrsiNeupit(string neUpit)
{
    int afektovano = 0;

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\A10RibolovackoDrustvo_Baza.mdf;Integrated Security=True";
    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda = new SqlCommand(neUpit,konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
            konekcija.Close();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
 public void PopuniListBox()
 {
     listBox1.Items.Clear();

     string upit = $@"select p.PecarosID as 'Sifra', FORMAT(p.PecarosID,'D3')+' '+
         p.Ime+' '+p.Prezime+' '+p.Adresa+' '+g.Grad+' '+p.Telefon as 'Podaci' " +
         "from Pecaros as p " +
         "inner join Grad as g " +
         "on p.GradID = g.GradID " +
         "ORDER BY PecarosID ASC";

     DataTable dt = Baza.IzvrsiUpit(upit);

     listBox1.DataSource = dt;
     listBox1.ValueMember = "Sifra";
     listBox1.DisplayMember = "Podaci";   
 }

 public void PopuniComboBox()
 {
     cmbGrad.Items.Clear();

     string upit = "select GradID as id, Grad as naziv from grad " +
         "ORDER BY Grad ASC";

     DataTable dt= Baza.IzvrsiUpit(upit);
     cmbGrad.ValueMember = "id";
     cmbGrad.DisplayMember = "naziv";
     cmbGrad.DataSource = dt;
 }
 private void Form1_Load(object sender, EventArgs e)
 {
    PopuniListBox();
    PopuniComboBox();

     string upit = $@"select p.PecarosID , p.Ime, p.Prezime, p.Adresa, g.Grad, p.Telefon  " +
         "from Pecaros as p " +
         "inner join Grad as g " +
         "on p.GradID=g.GradID " +
         "ORDER BY PecarosID ASC";

     DataTable dt = Baza.IzvrsiUpit(upit);
     if(dt.Rows.Count > 0 )
     {
         txtSifra.Text = dt.Rows[0][0].ToString();
         txtSifra.Enabled = false;
         txtIme.Text = dt.Rows[0][1].ToString();
         txtPrezime.Text = dt.Rows[0][2].ToString();
         txtAdresa.Text= dt.Rows[0][3].ToString();
         cmbGrad.Text= dt.Rows[0][4].ToString();
         txtTelefon.Text = dt.Rows[0][5].ToString();
     }

 }
----------------------------------------------------------A12-Baza.cs-
public static DataTable IzvrsiUpit(string upit)
{
    DataTable dt = new DataTable();

    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Baza_A12FudbalskiStadioni.mdf;Integrated Security=True";

    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlDataAdapter da = new SqlDataAdapter(upit,konekcija))
        {
            da.Fill(dt);
        }
    }
        return dt;
}

public static int IzvrsiNeupit(string neUpit)
{
    int afektovano = 0;
    string konekcioniString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Baza_A12FudbalskiStadioni.mdf;Integrated Security=True";
    using (SqlConnection konekcija = new SqlConnection(konekcioniString))
    {
        using (SqlCommand komanda= new SqlCommand(neUpit,konekcija))
        {
            konekcija.Open();
            afektovano = komanda.ExecuteNonQuery();
        }
    }
    return afektovano;
}
------------------------------------------------Upis u list view/box/combobox
public void RefreshListView()
{
    listView1.Items.Clear();

  string upit1 = "select s.StadionID, s.Naziv, g.Grad, " +
        "s.Kapacitet, s.Adresa, s.BrojUlaza " +
        "from Stadion s left join Grad g " +
        "on s.GradID=g.GradID";

    DataTable dt = Baza.IzvrsiUpit(upit1);

    foreach (DataRow red in dt.Rows)
    {
        string[] podaci =
        {
            red[0].ToString(),
            red[1].ToString(),
            red[2].ToString(),
            red[3].ToString(),
            red[4].ToString(),
            red[5].ToString()
        };

        ListViewItem stavka = new ListViewItem(podaci);
        listView1.Items.Add(stavka);
    }
}

public void PopunjavanjeComboBoxa()
{
    cmbGrad.Items.Clear();

    string upit2 = "select GradID as id, Grad as ime from Grad";
    DataTable dt = Baza.IzvrsiUpit(upit2);

    cmbGrad.DataSource = dt;
    cmbGrad.ValueMember = "id";
    cmbGrad.DisplayMember = "ime";

    foreach (DataRow red in dt.Rows)
    {
        cmbGrad.Items.Add(red[1].ToString());
    }
}

private void Form1_Load(object sender, EventArgs e)
{
    RefreshListView();
    listView1.FullRowSelect = true;
    listView1.MultiSelect = false;
    PopunjavanjeComboBoxa();
}






















