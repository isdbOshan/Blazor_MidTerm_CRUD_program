# Blazor_MidTerm_CRUD_program


Blazor CRUD program. 
Blazor is a framework for building interactive client-side web UI with .NET:

Create rich interactive UIs using C# instead of JavaScript.
Share server-side and client-side app logic written in .NET.
Render the UI as HTML and CSS for wide browser support, including mobile browsers.
Integrate with modern hosting platforms, such as Docker.
Build hybrid desktop and mobile apps with .NET and Blazor.
Using .NET for client-side web development offers the following advantages:

Write code in C# instead of JavaScript.
Leverage the existing .NET ecosystem of .NET libraries.
Share app logic across server and client.
Benefit from .NET's performance, reliability, and security.
Stay productive on Windows, Linux, or macOS with a development environment, such as Visual Studio or Visual Studio Code.
Build on a common set of languages, frameworks, and tools that are stable, feature-rich, and easy to use.


namespace Evidence_Mid_11.Shared.Models
{
    public class Device
    {
        public int DeviceId { get; set; }
        [Required, StringLength(50)]
        public string DeviceName { get; set; } = default!;
        [Required, Column(TypeName = "date")]
        public DateTime ReleaseDate { get; set; } = DateTime.Today;
        [Required, Column(TypeName = "money")]
        public decimal Price { get; set; }
        public bool OnSale { get; set; }
        [Required, StringLength(30)]
        public string Picture { get; set; } = default!;
        public virtual ICollection<Spec> Specs { get; set; } = new List<Spec>();
    }
    public class Spec
    {
        public int SpecId { get; set; }
        [Required, StringLength(30)]
        public string SpecName { get; set; } = default!;
        [Required, StringLength(50)]
        public string Value { get; set; } = default!;
        [Required, ForeignKey("Device")]
        public int DeviceId { get; set; }
        public virtual Device? Device { get; set; } = default!;
    }
    public class DeviceDbContext : DbContext
    {
        public DeviceDbContext(DbContextOptions<DeviceDbContext> options) : base(options) { }
        public DbSet<Device> Devices { get; set; } = default!;
        public DbSet<Spec> Specs { get; set; } = default!;
        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Device>().HasData(
                new Device { DeviceId=1, DeviceName="iPhone 11", ReleaseDate=new DateTime(2020, 12, 1), OnSale=true, Picture="1.jpg", Price=67000.00M}
                );
            modelBuilder.Entity<Spec>().HasData(
                new Spec { SpecId=1, DeviceId=1, SpecName="Storage", Value="32GB"},
                new Spec { SpecId = 2, DeviceId = 1, SpecName = "RAM", Value = "4GB" }
                );
        }
    }
}
