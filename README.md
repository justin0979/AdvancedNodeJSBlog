# Blog setup for Stephen Grider's Udemy Course "NodeJS: Advanced Concepts"

The `client` directory is NOT using `create-react-app`.
If you want to use `create-react-app` instead of this current `client`,

- just move the `src` directory to the root with `mv src ..`
- then change dir to root of project with `cd ..`
- erase `client` with `rm -r client`
- create new client with `npx create-react-app clien` (or whatever else is used)
- mv `src` to client with `mv src client` erase CRA `src` with Stephen's.

I used this same `client` code for Stephen's course "Node with React: Fullstack
Web Development" and was able to successfully complete the course with everything
working on both development and production (on heroku). Below mentions issues that
can occur (though nothing really specific because I can't remember each issue).

### There is a possiblity of needing to install extra packages during course.

When I was taking "Node with React: Fullstack Web Development", I did run into
issues with webpack and other packages that I needed to install (like
`dotenv-webpack` needing to be installed in the `client` directory). I'm
comfortable with using webpack (the client side uses `webpack-dev-server`) and so
when trying to run `npm run dev`, the webpack dev server usually specifically
said which package was needed. However, I had to look up how to use those packages,
which was usually very straight forward in the doc's.

Other issues that weren't specifically stated, I just googled what I was trying to
do and what errors were showing up and there were always answers to how to fix
them.
