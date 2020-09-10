# django-tuto
django-tuto
# How to Write Efficient Views, Models, and Queries in Django
![alt text](https://www.freecodecamp.org/news/content/images/size/w2000/2020/07/cover.png)
__I like Django. It’s a well-considered and intuitive framework with a name I can pronounce out loud. You can use it to quickly spin up a weekend-sized project, and you can also use it to run full-blown production applications at scale.
I’ve done both of these things, and over the years I’ve discovered how to use some of Django’s features for maximum efficiency. These are:__
	*Class-based versus function-based views
	*Django models
	*Retrieving objects with queries

#Class-based versus function-based views

__Remember that Django is all Python under the hood. When it comes to views, you’ve got two choices: view functions (sometimes called “function-based views”), or class-based views.
Years ago when I first built ApplyByAPI, it was initially composed entirely of function-based views. These offer granular control, and are good for implementing complex logic. Just as in a Python function, you have complete control (for better or worse) over what the view does.
But with great control comes great responsibility, and function-based views can be a little tedious to use. You’re responsible for writing all the necessary methods for the view to work - this is what allows you to completely tailor your application.
In the case of ApplyByAPI, there were only a sparse few places where that level of tailored functionality was really necessary. Everywhere else, function-based views began making my life harder. Writing what is essentially a custom view for run-of-the-mill operations like displaying data on a list page became tedious, repetitive, and error-prone.
With function-based views, you’ll need figure out which Django methods to implement in order to handle requests and pass data to views. Unit testing can take some work to write. In short, the granular control that function-based views offer also requires some granular tedium to properly implement.
I ended up holding back ApplyByAPI while I refactored the majority of the views into class-based views. This was not a small amount of work and refactoring, but when it was done, I had a bunch of tiny views that made a huge difference. I mean, just look at this one:__

'<class ApplicationsList(ListView):
    model = Application
    template_name = "applications.html">'

__It’s three lines. My developer ergonomics, and my life, got a lot easier.
You may think of class-based views as templates that cover most of the functionality any app needs. There are views for displaying lists of things, for viewing a thing in detail, and editing views for performing CRUD (Create, Read, Update, Delete) operations.
Because implementing one of these generic views takes only a few lines of code, my application logic became dramatically succinct. This gave me less repeated code, fewer places for something to go wrong, and a more manageable application in general.
Class-based views are fast to implement and use. The built-in class-based generic views may require less work to test, since you don’t need to write tests for the base view Django provides. (Django does its own tests for that; no need for your app to double-check.)
To tweak a generic view to your needs, you can subclass a generic view and override attributes or methods. In my case, since I only needed to write tests for any customizations I added, my test files became dramatically shorter, as did the time and resources it took to run them.
When you’re weighing the choice between function-based or class-based views, consider the amount of customization the view needs, and the future work that will be necessary to test and maintain it.
If the logic is common, you may be able to hit the ground running with a generic class-based view. If you need sufficient granularity that re-writing a base view’s methods would make it overly complicated, consider a function-based view instead.__

#Django models

'<class StaffMember(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    company = models.OneToOneField(Company, on_delete=models.CASCADE)

    def __str__(self):
        return self.company.name + " - " + self.user.email>'





