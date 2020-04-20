# Don't use `using namespace std`

Back in Uni, I was taught to always use `using namespace std` on top of my C++ files, after the include statements, in order to make things like `cout` easily available. However, according to the Google C++ style guide, this isn't a good idea. Instead, be more specific and use `using std::cout` or `using std::endl`, or simply `std::cout` and `std::endl` when only used once or twice. 
