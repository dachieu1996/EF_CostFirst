# CostFirst

## Install EntityFramework: 
<pre>
Install-Package EntityFramwork
</pre>

## Add connection string on App.config
`<connectionStrings>
    <add name="DefaultConnection" connectionString="Data Source=DacHieu; initial catalog=PlutoCodeFirst; User Id=sa; Password=" providerName="System.Data.SqlClient"/>
</connectionStrings>`

## Sample Model
<pre>
public class Course
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Description { get; set; }
        public CourseLevel Level { get; set; }
        public float FullPrice { get; set; }
        public Author Author { get; set; }
        public IList<Tag> Tags { get; set; }
    }

    public class Author
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public IList<Course> Courses { get; set; }
    }

    public class Tag
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public IList<Course> Courses { get; set; }
    }

    public enum CourseLevel : byte
    {
        Beginning = 1,
        Intermediate = 2,
        Advanced = 3
    }

    public class PlutoContext : DbContext
    {
        public DbSet<Course> Courses { get; set; }
        public DbSet<Author> Authors { get; set; }
        public DbSet<Tag> Tags { get; set; }

        public PlutoContext()
            : base("name=DefaultConnection")
        {
            
        }
    }
</pre>
> Note: Must have class adopt DbContext to Initial migration (In this case: PlutoContext)

## Run migration and update database
<pre>
enable-migrations
</pre>
<pre>
add-migration InitialModel
</pre>
<pre>
update-database
</pre>
