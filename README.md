# Go Language - Movies CRUD

This is a CRUD application to learn Go Language. It is a simple application to manage movies using **Slices**.

## Table of contents

- [Go Language - Movies CRUD](#go-language---movies-crud)
  - [Table of contents](#table-of-contents)
  - [Overview](#overview)
  - [My process](#my-process)
    - [Built with](#built-with)
    - [What I learned](#what-i-learned)
    - [Continued development](#continued-development)
    - [Useful resources](#useful-resources)

## Overview

- ### System Overview Diagram

![](./screenshots.png)

![System Overview Diagram](https://user-images.githubusercontent.com/77122922/230974281-62761883-aa63-4e07-a918-8580ecc818b1.png)

![](./screenshot.jpg)

- ### Screenshot

**Get All Movies**
![Get All Movies](https://user-images.githubusercontent.com/77122922/230964237-48142d1f-ff95-49b8-b334-7d07c0587c18.png)

**Get Movie By ID**
![Get Movie By ID](https://user-images.githubusercontent.com/77122922/230964426-fc5d6ed7-356a-4142-ad90-fb1104a3da71.png)

**Create Movie**
![Create Movie](https://user-images.githubusercontent.com/77122922/230965086-da489cd8-28cb-44c9-818f-b597aa0546a3.png)

**Update Movie**
![Update Movie](https://user-images.githubusercontent.com/77122922/230965424-151416e6-7215-4ed2-9c91-3494d62b4164.png)

**Delete Movie**
![Delete Movie](https://user-images.githubusercontent.com/77122922/230965587-f8e9918d-5436-4d56-8bc6-a90d9aee22c4.png)

## My process

### Built with

- [Go Language](https://golang.org/)
- [Gorilla Mux](https://github.com/gorilla/mux)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Postman](https://www.postman.com/) - API testing tool

### What I learned

In this project, I learned how to create a simple CRUD application using Go Language. I learned how to use Slices and how to use Gorilla Mux to create a REST API.

Create a movie function code snippet:

```go
func createMovie(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	var movie Movie
	_ = json.NewDecoder(r.Body).Decode(&movie)
	movie.ID = strconv.Itoa(rand.Intn(100000000000))
	movies = append(movies, movie)
	json.NewEncoder(w).Encode(movie)
}
```

Get all movies function code snippet:

```go
func getAllMovies(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json") //convert struct to json
	json.NewEncoder(w).Encode(movies)                  //encode the movies to json
}
```

Get movie by ID function code snippet:

```go
func getMovie(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	params := mux.Vars(r)
	for _, movie := range movies {
		if movie.ID == params["id"] {
			json.NewEncoder(w).Encode(movie)
			return
		}
	}
}
```

Update movie function code snippet:

```go
func updateMovie(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	params := mux.Vars(r)
	for index, movie := range movies {
		if movie.ID == params["id"] {
			movies = append(movies[:index], movies[index+1:]...) //delete the movie
			var movie Movie
			_ = json.NewDecoder(r.Body).Decode(&movie)
			movie.ID = params["id"]
			movies = append(movies, movie)
			json.NewEncoder(w).Encode(movie)
			return
		}
	}
}
```

Delete movie function code snippet:

```go
func deleteMovie(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	params := mux.Vars(r)
	for index, movie := range movies {
		if movie.ID == params["id"] {
			movies = append(movies[:index], movies[index+1:]...) //delete the movie
			break
		}
	}
	json.NewEncoder(w).Encode(movies)
}
```

### Continued development

I will continue to learn Go Language and create more projects using Go Language. Also I hope to continue this project with a Database.

### Useful resources

- [Golang Tutorial for Beginners | Full Go Course](https://youtu.be/yyUHQIec83I) - This helped me to learn the basics of Go Language. I really liked this video and found it very useful.
