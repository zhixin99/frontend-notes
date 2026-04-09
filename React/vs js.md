## join
* In React, it reads HTML-like syntax directly. It can also read html syntax in an array, So no need to join("")
```jsx
const projectContainerEl = projectsData.map( project => (
    <ProjectCard
        header={project.header}
        src={project.src}
        alt={project.alt}
        liveLink={project.liveLink}
        codeLink={project.codeLink}
        date={project.date}
        description={project.description}
    />
))
```
* In Javascript, innerHTML is expected a string, so use join("") to convert the array to a string

## quotes
* In react, never add quotes to a javascript. Otherwise it will take the whole thing as a string.
```jsx
return (
    dataList.map(data => (
        <div key={item.id}>
        </div>
    ))
)
```
* In Javascript, add quotes to `variable attribute values` in `template string` is a good habit.
```js
src = "xxx"
container.innerHTML = `<img src="${src}">`
```
