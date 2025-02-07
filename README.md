 [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
 [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
 

# Tomorrow_io
Provides a wrapper layer for interfacing with [Tomorrow.io](https://tomorrow.io). 
This is not an official package, and is primarily written for use in 
[HomeAssistant](https://home-assistant.io) plugins.

# Useage
You will need to get an API key from Tomorrow.io. [Sign up](https://www.tomorrow.io/weather-api/),
then navigate to the [keys](https://app.tomorrow.io/development/keys) page to get your API key. 
Note that the free plan limits you to 500 requests/day and 25 requests/hour.

Once you have an API key, you can simply create a `Tomorrow` object, and start pinging the API. 
A few examples follow.

## Examples
### Defaults
By default, the package assumes you want to know about Iowa State University. You can change that by
passing the `longitude` and `latutude` arguments to any of Tomorrow's functions. To set your own defaults,
pass them to the `__init__` call. For prettymuch everything else, it assumes you want to follow Tomorrow.io's
defaults, from their [API docs](https://docs.tomorrow.io/reference/welcome).
#### Get the current temperature
 ```python
from tomorrow_io import Tomorrow

apikey = 'YOUR_API_KEY'

tomorrow = Tomorrow(apikey)
tomorrow.get_current(data_fields=['temperature'])
```

#### Set a default location
 ```python
from tomorrow_io import Tomorrow

apikey = 'YOUR_API_KEY'

# Check in on the Hawkeyes, may they always have rain on gameday!
tomorrow = Tomorrow(apikey, longitude=-91.5549009294, latitude=41.6626978351)
tomorrow.get_current(data_fields=['weatherCode'])
```
Note that we can still override the default location by passing latitude and/or longitude any of the functions
of `Tomorrow`.

## data_fields
To get the information you want, you have to ask for it. Tomorrow.io supports numerous data fields, so I won't
list them all, but some of the most common ones are below. A full list can be found 
[here](https://docs.tomorrow.io/reference/data-layers-overview)

```
temperature
temperatureApparent
humidity
precipitationProbability
precipitationType
cloudCover
weatherCode
epaIndex
epaHealthConcern
weedIndex
grassIndex
treeIndex
```

# FAQ
### Why bother with this though? Aren't API calls pretty easy?
Yep. The only real reason this exists is to facilitate Home Assistant plugin development.
They require that API calls be wrapped in a library, available on PyPi. 
[Source](https://developers.home-assistant.io/docs/creating_component_code_review#4-communication-with-devicesservices)

### Why black? That makes all this code look really dumb!
Yeah, I agree. Trying it out, since the Home Assistant project uses it, and I figured I should get used to it.

### Pip install fails with `file not foud: setup.py` or similar
Your pip is out of date. `pip install --upgrade pip` (requires at least pip version 19, 
[link](https://setuptools.readthedocs.io/en/latest/setuptools.html#setup-cfg-only-projects))

### This FAQ seems like a list of reasons not to use this
Yes it does, doesn't it?