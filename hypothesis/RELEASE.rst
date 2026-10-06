RELEASE_TYPE: patch

This patch makes :func:`~hypothesis.strategies.from_regex` default to an ASCII-only
alphabet when the pattern is compiled with :obj:`python:re.ASCII`. Previously,
patterns such as ``st.from_regex(re.compile(r"\w+", re.ASCII))`` could generate
non-ASCII characters (for example in padding around the match or for ``.``);
generated strings are now always ASCII-only and therefore suitable for
ASCII-only consumers. Patterns which require non-ASCII characters raise a clear
:class:`~hypothesis.errors.InvalidArgument` error, and an explicit ``alphabet=``
argument continues to override the default.
