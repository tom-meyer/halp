### Mocks, spies, and stubs, oh my!

(From https://martinfowler.com/articles/mocksArentStubs.html)

Meszaros uses the term Test Double as the generic term for any kind of pretend
object used in place of a real object for testing purposes. The name comes from
the notion of a Stunt Double in movies. (One of his aims was to avoid using any
name that was already widely used.) Meszaros then defined four particular kinds
of double:

 - **Dummy** objects are passed around but never actually used. Usually they are just
   used to fill parameter lists.

 - **Fake** objects actually have working implementations, but usually take some
   shortcut which makes them not suitable for production (an in memory database is
   a good example).

 - **Stubs** provide canned answers to calls made during the test, usually not
   responding at all to anything outside what's programmed in for the test.

 - **Spies** are stubs that also record some information based on how they were
   called. One form of this might be an email service that records how many
   messages it was sent.

 - **Mocks** are what we are talking about here: objects pre-programmed with
   expectations which form a specification of the calls they are expected to
   receive.
