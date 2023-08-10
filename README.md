
# SimulateUser Django App

## General Details

### Description

The SimulateUser Django app provides developers with a robust toolset to simulate user experiences within their web applications. By impersonating a specific user or even an anonymous user, developers can observe user experiences firsthand, enabling easier debugging, testing, and understanding of user interfaces and functionality.

### Features
- **Private Tags Functionality**: Safeguard sensitive content in templates with `{% private %}` and `{% privateblock %}` tags.
    ```html
    <p>{% private 'Some Content that should be private' %}</p>
    ```
    ```html
    {% privateblock %}
    <p>Some Content that should be private</p>
    <p>Some Content that should be private</p>
    <p>Some Content that should be private</p>
    {% endprivateblock %}
    ```

 - **Fully Simulated Sessions**: Impersonate any user in the system, including anonymous users, with a complete session simulation.

 - **Transparency with Notifications & Logs**: Stay informed about all simulation activities through comprehensive notifications and logs.

 - **Customizable with Settings**: Tweak the app behavior according to project requirements. It's important to note that this app should not be used in production environments due to potential security concerns.

 - **Extendable Template with UI**: An aesthetically pleasing user interface for switching users is available in the simulate_user_base.html template, which can be extended by any template in your project.

## Setup Instructions
1. **Install the App**:

    ```
    pip install django-simulate-user
    ```

2. **Add the App**: 
Include 'simulateuser' in your INSTALLED_APPS setting.

    ```python
    INSTALLED_APPS = [
        ...
        'simulate_user',
        ...
    ]
    ```

3. **Add the URLs**:
Ensure that you add the app's URL configurations to your project's urls.py:

    ```python
    urlpatterns = [
        ...
        path('simulate_user/', include('simulate_user.urls')),
        ...
    ]
    ```

4. **Middleware and Context Manager**:
Ensure you add the necessary middleware and context manager for the app in the respective Django settings:
    ```python
    MIDDLEWARE = [
        ...
        'simulate_user.middleware.SimulateUserMiddleware',
        ...
    ]
    ```
    
    ```python
    TEMPLATES = [
        {
            ...
            'OPTIONS': {
                'context_processors': [
                    ...
                    'simulate_user.context_processors.simulate_user_context', 
                    ...
                ],
            },
            ...
        },
    ]
    ```

5. **Database Migrations**:
After integrating the app, run:

    ```
    python manage.py makemigrations
    python manage.py migrate
    ```

## Configuration
Simulate User has many different settings that you can control to ensure that your Simulate User experience is exactly the solution your project needs.

- **Enable or Disable Simulate User**: 
By default, Simulate User is enabled. This means that the UI and entire feature set supplied by the Simulate User is working as designed. However, you can disable it. To disable Simulate User, you simply need to have the following line in your settings file and set it to False.
We highly recommend against leaving Simulate User enabled in production.
    ```python
    ENABLE_SIMULATE_USER: bool = True
    ```
  
- **Set Authentication Backend**:
If you use an authentication backend other than the default backend, you should alter the simulate user backend with the path for the one that it should use. By default, it is set to use the django default authentication backend. However, if you use different backends, it might be necessary to make Simulate User use the correct one.
    ```python
    SIMULATE_USER_AUTHENTICATION_BACKEND: str = 'django.contrib.auth.backends.ModelBackend'
    ```
  
- **Restrict Actions of Staff Members in Simulation Mode**:
By default, Simulate User only allows GET requests to be done in simulation mode. This is for security and safety purposes. However, you can change this by toggling the setting:
    ```python
    ONLY_ALLOW_SIMULATED_GET_REQUESTS: bool = True
    ```
  
- **Set Custom Private Replacement Text**:
By default, Simulate User replaces all text in private tags with 'HIDDEN FOR USER PRIVACY PURPOSES'. However, you can change that using the following setting:
    ```python
    PRIVATE_CONTENT_REPLACEMENT: str = 'HIDDEN FOR USER PRIVACY PURPOSES'
    ```
  
- **Set Custom Session Settings**:
By default, Simulate User sets all simulated sessions to last for a maximum of 3600 seconds. It also automatically deletes all simulated sessions and simulated session actions for 14 days. You can toggle those settings as follows:
    ```python
    SIMULATED_SESSION_EXPIRY: int = 3600
    SIMULATED_SESSION_RETENTION: int =  14
    ```

- **Set Who Can See and Use Simulated User**:
By default, Simulate User is set to be enabled for all users who have the is_staff attribute as True. However, you can change this by using any bool attribute of your user model. You can create your own for maximum integration. You can toggle the following setting:
    ```python
    SIMULATED_USER_CONTROL_CONDITION: str = 'is_staff'
    ```

## Contributing
As this is an open-source project hosted on GitHub, your contributions and improvements are welcome! Follow these general steps for contributing:

1. **Fork the Repository**: 
Start by forking the main repository to your personal GitHub account.

2. **Clone the Forked Repository**: 
Clone your forked repository to your local machine.

    ```
    git clone https://github.com/YidiSprei/SimulateUserProject.git
    ```

3. **Create a New Branch**: 
Before making any changes, create a new branch:

    ```
    git checkout -b feature-name
    ```

4. **Make Your Changes**: 
Implement your features, enhancements, or bug fixes.

5. **Commit & Push**:

    ```
    git add .
    git commit -m "Descriptive commit message about changes"
    git push origin feature-name
    ```
   
6. **Create a Pull Request (PR)**: 
Go to your forked repository on GitHub and click the "New Pull Request" button. Make sure the base fork is the original repository, and the head fork is your repository and branch. Fill out the PR template with the necessary details.

Remember to always be respectful and kind in all interactions with the community. It's all about learning, growing, and helping each other succeed!

## Credits
Developed with 💙 by Yidi Sprei. We thank all the contributors and the Django community for their support and inspiration.

