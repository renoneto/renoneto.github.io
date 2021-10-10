---
layout: post
title:      "Using streamlit to show your project"
date:       2021-10-08 13:49:12 +0000
permalink:  using_streamlit
---

As a data scientists, we need to constantly show the result of our work to our stakeholders. Either through charts, dashboards, Jupyter notebooks or PowerPoint presentations. However, wouldn't it be great if we could create an interactive App? I give the stakeholders a _feel_ for what we have built? Letting them play with it?

That's where Streamlit comes to help! 

## Why Streamlit?
Streamlit was founded by a group of data scientists who know the struggles! It helps us to focus on the insights/capabilities of what we are trying to share rather than having to remember again how to create a dual-axis chart in matplotlib or creating functions in notebooks so users can interact with what was built.

## What is Streamlit?
According to their website: _Streamlit is an open-source Python library that makes it easy to create and share beautiful, custom web apps for machine learning and data science. In just a few minutes you can build and deploy powerful data apps._

## My Use Case
Okay, that's all cool but let's get to what really matters: _How could you use it?_
To answer that question, I'm going to go through an example of a project where I have decided to use Streamlit.

I have created a movie-recommender using the [MovieLens dataset](https://grouplens.org/datasets/movielens/). I'm not going to get into the actual model that I'm using (it's a Singular Valua Decomposition model, if you're wondering) but rather focus on how I'm benefiting from Streamlit to show what I have created.

### My problem
I had a model that was providing some recommendations but it was very hard to interact with it. I even created a function taking inputs to help me out but it wasn't enough. It was still too complicated and I had to run it on a Jupyter Notebook to make it work. So I thought, _Wouldn't it be great if I could have it as an app?_

That's when I found Streamlit! At this point, you are probably asking where you can see the app so decide if it's worth reading the rest of my post. [Here it is](https://movie-recommender-reno.herokuapp.com/).

[You can find the full code here](https://github.com/renoneto/fourth_module_project/blob/main/my_app.py). But I'm going to focus on my main learnings.

## Main Streamlit Commands
At this point, I invite you to have my app open and see some commands that I have used and visually identify them in the app.

#### `set_page_config`
It sets the name of your app in the browser tab with the option of changing the layout ('wide' or 'centered').
> App command: `set_page_config(page_title="Movies Recommendation")`

#### `write`
I takes markdown text and displays it. I have used it in several places.
> App command: `write('# What movies to watch next? :clapper:')`

#### `selectbox`
Displays a dropdown taking an input from the user.
> App command: `selectbox('Genres:', genres)`

#### `warning` + `stop`
Displays a warning message. You can use it in combination with an if statement and `stop` to stop the app until a criteria is met. 
> App command: 
> ```
> # If no genre is selected stop the app from running the rest
> if selected_genre == '-':
>	st.warning('Please choose a genre')
>	st.stop()
>	```

#### `form` + `form_submit_button`
A form is a container that visually groups other elements and widgets together, and contains a Submit button. When the form’s Submit button is pressed, all widget values inside the form will be sent to Streamlit in a batch. 

In my app, I have used it to combine all ratings for all movies. Initially, I didn't have a form, however, that was creating other issues since I was trying to get five ratings from the user and it was taking a long time to load all the images. With the form, all ratings would load at the same time which gives the user a better experience. 

In addition, without the form, after every rating was collected the whole app would run again, which would load the images again and decrease the user experience. So with the form, I found a way to display all ratings and only run the rest of the code when the 'Show recommendations!' button was clicked.
> App command:
> ```
> with st.form(key='form'):
> ...
> form_submit_button('Show recommendations!')
> ```

#### `columns` + `image`
With the `columns` command is possible to create multiple widgets side-by-side. I'm using it to have the picture (`image` command) and rating side-by-side, for example.
> ```
> # For each movie create three columns
> 	row1_0, row1_1, row1_2 = st.columns((1,2,3))
> 
> 	# The first will contain the image
> 	with row1_1:
> 		st.image(movie_image_links[i], width=150)
> 
> 	# Second will have the rating radio form
> 	with row1_2:
> 		st.radio(movie_to_rate_title, ratings_options, key=i)
> ```

# Conclusion
This was my first app using Streamlit so there's definitely more to learn. However, I invite you to look at the code and see how I'm building the app. You will see how easy it was to do it. 
