## Blog setup for Stephen Grider's Udemy Course "NodeJS: Advanced Concepts"

### Remember to add `config/dev.js` to `.gitignore` after updating keys.

### Also, remember that config/dev.js does NOT have your mongoURI key

Additions to `.gitignore` might still be tracked by `.git`, so run the
following:</br>
`git rm --cached .`</br>
`git add .`</br>
`git commit -m "git should no longer tracks files added to .gitignore from this point foward"`</br>

## To Run Dev Load packages for both server and client

`npm run loadpkgs` (this runs `npm i && npm i --prefix client`)

### Run development

`npm run dev`

### Client is NOT using CRA

The `client` directory is NOT using `create-react-app`.
I only used this client version because it loads faster than CRA (the app
only needs CRA to load once, but I use that client for lots of other dev things and it just saves time with my computer).
If you want to use `create-react-app` instead of this current `client`,

- just move the src directory to the root dir of project with `mv src ..`
- then change dir to root of project with `cd ..`
- erase client dir with `rm -r client`
- create new client with `npx create-react-app client` (or whatever is preferred)
- mv src dir to client dir with `mv src client`, this will erase CRA's `src` with Stephen's.

I used this same `client` code for Stephen's course "Node with React: Fullstack
Web Development" and was able to successfully complete the course with everything
working on both development and production (on heroku). Below mentions issues that
can occur (though nothing really specific because I can't remember each issue).

### There is a possiblity of needing to install extra packages during course, some of which refer to Fixes sections from Fullstack course.

When I was taking "Node with React: Fullstack Web Development", the course
had several `Fixes` sections to address old code. Even though I've run
this current Blog code without any noticable issues, there might be problems needing
fixes that may have been addressed in the Fullstack course. As I go along in this course, I'll try to update this base code.

Also I did run into issues from the Fullstack course with webpack and other packages that I needed
to install (like `dotenv-webpack` needing to be installed in the `client`
directory) that should not cause issues with this AdvancedJS course. I'm comfortable with using webpack (the client side uses
`webpack-dev-server`) and so
when trying to run `npm run dev`, the webpack dev server will usually specifically
state which package was needed. However, I had to look up how to use those packages,
which was usually very straight forward in the doc's.

Other issues that weren't specifically stated, I just googled what I was trying to
do and what errors were showing up and there were always answers to how to fix
them. So, if you don't feel comfortable directly working on webpack.config.js files (or even babel.config.js), then CRA is a good option.

### Problems I immediately ran into and fixed

- materialize-css icons not showing up, fixed by adding `link` tag to html
- proxy issue, reconfigured path in webpack.config.js line 28 from `/auth/google` to just `/auth`
- updated version of `passport-google-oauth20` from 1.0.0 to 2.0.0
- in root index.js, I commented out `mongoose.Promise = global.Promise` on line 12 b/c I recall ever having seen that taught or used and thought it might just be an old way of using mongoose. App still works with it commented out. If I see database persistance issues, I'll research more into that command.
- in root index.js, on line 14, change `useMongoClient: true` to `useNewUrlParser: true`. If I remember correctly, on running dev there would be a deprecation warning.
- in root index.js, line 15, added `useUnifiedTopology: true` to MongoClient constructor due to deprecation warning.

### Problems I left unsolved after hours of researching, just to have them work the next day

- Proxy issue after click "SAVE BLOG" in review. After clicking "SAVE BLOG", the blog would successfully be saved in the database, and would display in `/blogs` but the `history.push('/blogs')` (or another part) did not re-route from `/blogs/new` to `/blogs`. The page would stay on `/blogs/new` and all of the fields would still have the same info and that info would be saved to the database for however many times I clicked "SAVE BLOG" for. I attempted many changes to webpack-dev-server's proxy (like using [::1] in place of localhost). Nothing worked that night. The next day, the redirect to `/blogs` just worked. Regardless of using [::1] or localhost, everything I changed that didn't work the night before, worked the next day after just turning on the computer and going straight to this app and running it.

So, just becuase I have this problem as "solved", I have no explanation of why it works; therefore, if there is a redirection issue again, it will probably have something to do with how my webpack config is setup (and `withRouter` disagreeing with my setup).
