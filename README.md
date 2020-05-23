# xoto3

`xoto3` (pronounced zoto-three) is a layer of useful micro-utilities
for `boto3` (the AWS Python library) particularly suitable for
serverless development.

These come from years of experience developing a serverless platform
at XOi Technologies, and represent real production code.

### Features

Some of the features included:

- A more general purpose `boto3` paginator.

- Higher-level abstractions for DynamoDB, including:

  - a transactional single-item update that allows you to express your update
    transformation in pure Python
  - automatic safeguards against various sorts of data that DynamoDB won't accept.
  - transparent BatchGet and BatchWrite utilities that work around the
    many annoyances of `boto3` and DynamoDB itself.
  - composable query interfaces that make writing basic queries against DynamoDB fun.

- Cloudwatch Insights and Log Groups Query URL formatters.

- General-purpose AWS Lambda finalization code, to make sure buffered
  IO gets a chance to flush before your Lambda gets paused.

- Wrapper for SSM parameter puts and gets, including built-in support
  for parameter values larger than what SSM will accept by
  automatically splitting your values and reconstructing them on gets.

- A piped multiprocessing pool that actually works on AWS Lambda,
  without shared memory. Sure, you can only get ~2 VCPUs with max RAM,
  but 2 is better than 1 if you need to crunch some numbers (or
  generate lots of presigned URLs).

Various other utilities are included as well - feel free to poke through the source code.

None of these features "rely" on any of the others, so all of the
power is left in your hands. This is not a framework; just a set of
mostly pure-functional utilities, with a couple of handy wrappers for
`boto3` functions that perform IO.