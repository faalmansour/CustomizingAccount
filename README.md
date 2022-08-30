# CustomizingAccount
Customizing account/registration page on .net core 
- Create custom class ex.ApplicationUser and inherit from IdentityUser

```
public class ApplicationUser : IdentityUser
{
    public string StudentNo { get; set; }
}
```

- Use the ApplicationUser type as a generic argument for the context

```
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder builder)
    {
        base.OnModelCreating(builder);
    }
}
```
  
- Update Pages/Shared/_LoginPartial.cshtml and replace IdentityUser with ApplicationUser
```
@inject SignInManager<ApplicationUser> SignInManager
@inject UserManager<ApplicationUser> UserManager
```
 - Update Startup.ConfigureServices and replace IdentityUser with ApplicationUser

```
  services.AddDefaultIdentity<ApplicationUser>(options => options.SignIn.RequireConfirmedAccount = true)
  .AddEntityFrameworkStores<ApplicationDbContext>();  
  ```
  
  ### Add fields to registeration form ex.StudentNo
  -After creating custom class as mentioned above, create migeration and update-database
  -Saffolding Account folding by right clicking on Areas\Identity\Pages\Account folder => new => new scaffolded item ...
  -Select the pages that need the customization ex.registeration page
  -Add StudentNo field to Register.cshtml
  -Add StudentNo field to Input Class in Register.cs
  
  ```
  public string StudentNo { get; set; }
  ```
  
