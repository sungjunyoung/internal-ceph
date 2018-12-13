# internal-[ceph](https://github.com/ceph/ceph)


### Analysis

---

### Tracing
- Install [lttng](https://lttng.org/download/#build-from-source) tools, ust, modules

- Build Ceph from source
```bash
$ cd ${CEPHPATH}
$ ./do_cmake.sh -DWITH_BLKIN=ON -DWITH_OSD_INSTRUMENT_FUNCTIONS=ON
$ make j8

# start vstart (without dashboard)
$ LD_PRELOAD=/usr/lib/x86_64-linux-gnu/liblttng-ust-fork.so \
../src/vstart.sh --debug --new -x --localhost
```

- Create session & Start lttng daemon
```bash
$ lttng create ceph
```

- Check lttng user space tracing list
```bash
$ lttng list -u
UST events:
-------------

PID: 11806 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-mon
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 12592 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-osd
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 12277 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-osd
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 11717 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-mon
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 11762 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-mon
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 12907 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-osd
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)

PID: 11983 - Name: /home/sungjunyoung/Naver/sources/ceph/build/bin/ceph-mgr
      lttng_ust_tracelog:TRACE_DEBUG (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_LINE (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_FUNCTION (loglevel: TRACE_DEBUG_FUNCTION (12)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_UNIT (loglevel: TRACE_DEBUG_UNIT (11)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_MODULE (loglevel: TRACE_DEBUG_MODULE (10)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROCESS (loglevel: TRACE_DEBUG_PROCESS (9)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_PROGRAM (loglevel: TRACE_DEBUG_PROGRAM (8)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_DEBUG_SYSTEM (loglevel: TRACE_DEBUG_SYSTEM (7)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_INFO (loglevel: TRACE_INFO (6)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_NOTICE (loglevel: TRACE_NOTICE (5)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_WARNING (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ERR (loglevel: TRACE_ERR (3)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_CRIT (loglevel: TRACE_CRIT (2)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_ALERT (loglevel: TRACE_ALERT (1)) (type: tracepoint)
      lttng_ust_tracelog:TRACE_EMERG (loglevel: TRACE_EMERG (0)) (type: tracepoint)
      lttng_ust_tracef:event (loglevel: TRACE_DEBUG (14)) (type: tracepoint)
      lttng_ust_lib:unload (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_lib:load (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:end (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:debug_link (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:build_id (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:bin_info (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      lttng_ust_statedump:start (loglevel: TRACE_DEBUG_LINE (13)) (type: tracepoint)
      zipkin:timestamp (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_integer (loglevel: TRACE_WARNING (4)) (type: tracepoint)
      zipkin:keyval_string (loglevel: TRACE_WARNING (4)) (type: tracepoint)
```

- Enable events, start session
```bash
$ lttng enable-event -u -a
$ lttng start ceph
```

- Start any ceph operation
```bash
# example
$ echo TEST > ./test-obj
$ rados -p test-pool test test-obj test-obj
```

- Stop lttng tracing
```bash
$ lttng stop
```

- View lttng tracings
```
$ lttng view
```