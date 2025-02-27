![Sangria Logo](https://sangria-graphql.github.io/assets/img/sangria-logo.svg)

[Sangria](https://sangria-graphql.github.io/) is a scala [GraphQL](http://facebook.github.io/graphql/) library.

[![Scala CI](https://github.com/arturalkaim/sangria/actions/workflows/scala.yml/badge.svg?branch=main)](https://github.com/arturalkaim/sangria/actions/workflows/scala.yml)


SBT Configuration:

```scala
libraryDependencies += "org.sangria-graphql" %% "sangria" % "<latest version>"
```

You can find an example application that uses akka-http with sangria here:

https://github.com/sangria-graphql/sangria-akka-http-example

More info and the documentation can be found in the project home page:

[https://sangria-graphql.github.io/](https://sangria-graphql.github.io/)

I would also recommend you to check out [Sangria Playground](https://github.com/sangria-graphql/sangria-playground).
It is an example of GraphQL server written with Play framework and Sangria. It also serves as a playground,
where you can interactively execute GraphQL queries and play with some examples.

If you want to use sangria with [react-relay](https://facebook.github.io/relay) framework, then you also may be interested in [sangria-relay](https://github.com/sangria-graphql/sangria-relay).

Sangria is a spec compliant GraphQL implementation, so it works out of the box with [Apollo](https://github.com/apollographql/apollo-client), [Relay](https://facebook.github.io/relay/), [GraphiQL](https://github.com/graphql/graphiql) and other GraphQL tools and libraries.


## Hello World Example

In this example we will use [circe](https://github.com/circe/circe) JSON marshalling, so we also need to include following dependency:

```scala
libraryDependencies += "org.sangria-graphql" %% "sangria-circe" % "1.3.2"
```

The most simple Hello World application might look like this:

```scala
import sangria.schema._
import sangria.execution._
import sangria.macros._
import sangria.marshalling.circe._
import scala.concurrent.ExecutionContext.Implicits.global

val QueryType = ObjectType("Query", fields[Unit, Unit](
  Field("hello", StringType, resolve = _ => "Hello world!")
))

val schema = Schema(QueryType)

val query = graphql"{ hello }"

val result = Executor.execute(schema, query)

result.foreach(res => println(res.spaces2))
```

this example will print following result JSON:

```json
{
  "data" : {
    "hello" : "Hello world!"
  }
}
```

For more complex example, I would recommend you to check out the [Getting Started Tutorial](https://sangria-graphql.github.io/getting-started/).

## Issues, Bugs, Ideas

If you've got some interesting ideas to share or discovered a nasty bug, feel free to use
[Sangria's issue tracker](https://github.com/sangria-graphql/sangria/issues).
Also feel free to fork project and create the pull requests - they are highly appreciated!

If you are facing an issue and not sure what would be the best way to describe it, the I would recommend you to use [this minimal gist](https://gist.github.com/OlegIlyenko/4068ad92e008cd4b5def1baa4ec3a67c) as a template. 

## StackOverflow

In case you need some help or support, then you can use [StackOverflow](https://stackoverflow.com/questions/tagged/sangria) for this.
When you are [asking a question](https://stackoverflow.com/questions/ask?tags=scala,graphql,sangria),
be sure to add `scala`, `graphql` and `sangria` tags, so that other people can easily find them.

## Gitter & Mailing List 

For more general, lengthy discussions or pretty much anything else please join us in the 
[gitter chat](https://gitter.im/sangria-graphql/sangria) and [google groups](https://groups.google.com/forum/#!forum/sangria-graphql).

## Contribute

If you like the project and would like to support it or contribute to it, then you are very welcome to do so.
You can spread the word and tweet about the project or even better - create a small blog post, video, example project and show how you use sangria and GraphQL.
I'm pretty sure it would be interesting for many people.

Also you can contribute to [the documentation](https://github.com/sangria-graphql/sangria-website) or help others by answering questions on
[StackOverflow](https://stackoverflow.com/questions/tagged/sangria) or joining discussions on the [gitter chat](https://gitter.im/sangria-graphql/sangria).
It would be very helpful!

Not to mention the code itself. There is nothing more exciting than hacking some stuff together :)
So please feel free to materialize your ideas in form of code and send pull requests! 

## License

**Sangria** is licensed under [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
