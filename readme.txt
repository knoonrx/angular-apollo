https://codesandbox.io/s/zqq6nk0x6x


const { ApolloServer, gql } = require("apollo-server");

var coursesData = [
  {
    id: 1,
    title: "Angular - The Complete Guide",
    author: "Maximilian Schwarzmüller",
    description:
      "Master Angular (Angular 2+, incl. Angular 5) and build awesome, reactive web apps with the successor of Angular.js",
    topic: "Angular",
    url: "http://codingthesmartway.com/courses/angular2-complete-guide/"
  },
  {
    id: 2,
    title: "GraphQL with React: The Complete Developers Guide",
    author: "Stephen Grider",
    description:
      "Learn and master GraphQL by building real web apps with React and Node",
    topic: "React",
    url: "https://codingthesmartway.com/courses/graphql-react"
  },
  {
    id: 3,
    title: "The Complete Node.js Developer Course",
    author: "Andrew Mead, Rob Percival",
    description:
      "Learn Node.js by building real-world applications with Node, Express, MongoDB, Mocha, and more!",
    topic: "Node.js",
    url: "https://codingthesmartway.com/courses/nodejs/"
  },
  {
    id: 4,
    title: "Node.js, Express & MongoDB Dev to Deployment",
    author: "Brad Traversy",
    description:
      "Learn by example building & deploying real-world Node.js applications from absolute scratch",
    topic: "Node.js",
    url: "https://codingthesmartway.com/courses/nodejs-express-mongodb/"
  },
  {
    id: 5,
    title: "JavaScript: Understanding The Weird Parts",
    author: "Anthony Alicea",
    description:
      "An advanced JavaScript course for everyone! Scope, closures, prototypes, this, build your own framework, and more.",
    topic: "JavaScript",
    url: "https://codingthesmartway.com/courses/understand-javascript/"
  }
];

// var getCourse = function(root, { id }) {
//   return coursesData.filter(course => {
//     return course.id === id || 0;
//   })[0];
// };

var getAllCourses = function() {
  return coursesData;
};

// Construct a schema, using GraphQL schema language
const typeDefs = gql`
  type Query {
    allCourses: [Course]
    course(id: Int!): Course
  }
  type Course {
    id: Int
    title: String
    author: String
    description: String
    topic: String
    url: String
  }
`;

// Provide resolver functions for your schema fields
const resolvers = {
  Query: {
    allCourses: getAllCourses
    // course: getCourse()
  }
};

const server = new ApolloServer({
  typeDefs,
  resolvers
});

server.listen().then(({ url }) => {
  console.log(`🚀 Server ready at ${url}`);
});
