``` java
@RequestMapping("order-state.json")
    public void orderJson(@RequestParam("token") String token, HttpServletRequest request) throws IOException {
        String orderNo = redisService.get(RedisConstant.ORDER_TOKEN_PREFIX + token);
        if (StringUtilsExt.isEmpty(orderNo)) {
            return;
        }
        AsyncContext asyncContext = request.startAsync();
        asyncContext.addListener(new AsyncListener() {
            @Override
            public void onComplete(AsyncEvent asyncEvent) throws IOException {
                log.info("已完成订单，通知页面");
                OrderStateResp orderState = getOrderState(orderNo);
                asyncContext.getResponse().getWriter().write(JsonUtils.toJson(orderState));
                asyncContext.getResponse().getWriter().flush();
            }

            @Override
            public void onTimeout(AsyncEvent asyncEvent) throws IOException {
                log.warn("订单状态查询超时");
            }

            @Override
            public void onError(AsyncEvent asyncEvent) throws IOException {
                log.warn("订单状态查询期间出错");
                asyncEvent.getAsyncContext().getResponse().getWriter().write("error");
            }

            @Override
            public void onStartAsync(AsyncEvent asyncEvent) throws IOException {
                log.info("开启订单状态通知的异步线程");
            }
        });
        asyncContext.setTimeout(660000);
        ORDER_ASYNC_CONTEXT.put(orderNo, asyncContext);
    }

```

![image.png](0)
