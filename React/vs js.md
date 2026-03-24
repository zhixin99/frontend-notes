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
