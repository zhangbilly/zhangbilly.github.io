---
layout:     post
title:      "Spring Data Web 扩展"
subtitle:   "从请求中自动组装分页对象"
date:       2016-05-23
author:     "ZhangBilly"
header-img: "img/in-post/spring-data/green.jpg"
tags:
    - spring data
---

# Spring Data Web 扩展

Spring Data支持Web扩展，有几种用法，这里主要讲如何通过请求参数构造Pageable对象。

在之前，如果是分页接口，可能的写法如下

	@RequestMapping(value = "songlist", method = RequestMethod.GET)
	public @ResponseBody JsonResponse getSongListByName(@RequestParam(value = "pn", defaultValue = "1") int pageNumber,
			@RequestParam(value = "ps", defaultValue = "20") int pageSize,
			@RequestParam(value = "sortType", defaultValue = "auto") String sortType, Model model,
			HttpServletRequest request) {
		JsonResponse json = new JsonResponse();
		Map<String, Object> searchParams = new HashMap<String, Object>();
		String songName = request.getParameter(Song.SONGNAME);
		if (StringUtils.isNotBlank(songName)) {
			searchParams.put(Operator.LIKE + "_" + Song.SONGNAME, songName);
		}
		Page<Song> songList = songService.getSongs(searchParams, pageNumber, pageSize, sortType);
		json.successWithData("songs", songList);
		return json;
	}


其中`@RequestParam(value = "sortType", defaultValue = "auto") String sortType,@RequestParam(value = "pn", defaultValue = "1") int pageNumber,@RequestParam(value = "ps", defaultValue = "20") int pageSize`，这些参数都是和分页相关的，在后面我们我们会根据这些参数去构建一个分页的对象，而如果启用了web 扩展，就可以这样写了

	@RequestMapping(value = "songlist", method = RequestMethod.GET)
	public @ResponseBody JsonResponse getSongListBuyName(Model model, Pageable pageable, HttpServletRequest request) {
		JsonResponse json = new JsonResponse();
		Map<String, Object> searchParams = new HashMap<String, Object>();
		String songName = request.getParameter(Song.SONGNAME);
		if (StringUtils.isNotBlank(songName)) {
			searchParams.put(Operator.LIKE + "_" + Song.SONGNAME, songName);
		}
		Page<Song> songList = songService.getSongs(searchParams, pageable);
		json.successWithData("songs", songList);
		return json;
	}


在请求中，加入下面几个参数

| 参数   | 含义                                       |
| ---- | ---------------------------------------- |
| page | 第几页，从0开始，默认0                             |
| size | 每页的大小，默认20                               |
| sort | 排序字段，默认升序，可以在属性后面跟排序的方式，如：sort=lastname,asc |

spring会为我们拼装好分页的对象

## 启用Web扩展

#### 如果采用java 配置


	@Configuration
	@EnableWebMvc
	@EnableSpringDataWebSupport
	class WebConfiguration { }


#### 如果采用xml 配置

	<bean class="org.springframework.data.web.config.SpringDataWebConfiguration" />

我在我的工程中加入了上面XML配置，报了下面的错

`org.springframework.beans.BeanInstantiationException: Could not instantiate bean class [org.springframework.data.domain.Pageable]: Specified class is an interface`

后面查了一下，改为下面这种就可以了。

     <mvc:annotation-driven>
     	 ......
         <mvc:argument-resolvers>
             <bean class="org.springframework.data.web.PageableHandlerMethodArgumentResolver" /> 
         </mvc:argument-resolvers>
     </mvc:annotation-driven>


具体可以参考[stackoverflow上的回答](http://stackoverflow.com/questions/22135002/spring-data-does-not-handle-pageable-action-argument-creation)。