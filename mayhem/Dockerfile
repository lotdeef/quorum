# Build Geth in a stock Go builder container
FROM fuzzers/go-fuzz:1.2.0 as builder

ADD . quorum
WORKDIR quorum/tests/fuzzers

RUN cd ./bitutil && GO_ENABLED=0 go-fuzz-build -libfuzzer -o ../bitutil.a .
RUN clang -fsanitize=fuzzer bitutil.a -o bitutil.libfuzzer

FROM ubuntu:20.04
COPY --from=builder /go/quorum/tests/fuzzers/bitutil.libfuzzer /

# CMD ["./bitutil.libfuzzer"]