# Student_DBMS

Student Database Management System
Date Created:13/07/2021

Overview:
	This Simple Spring Boot Project is developed to maintain the students details who are all studying under their online academy and also the details of the course available in their online academy. 
Maintaining students’ details includes creating new student profile, update an existing profile and deleting student profile and also search a student’s detail. Maintaining courses’ details includes creating new course, update an existing course and remove available course. 
In this project, one can also maintain the fee details of each course and students’ fee detail of how much they paid and how much they need to pay.
This project also includes Junit Test Cases to test this spring boot project.
Recommended System Requirements:
 *) Windows/Linux/MacOS
 *)	Java SE Development Kit 11
 *)	Eclipse/Spring Tool Suite IDE Platform.

Sample Codes:
Sample of some Request Mapping:
	Request of adding new student:
@RequestMapping("/add")
	public ModelAndView add(int aid,String aname,String tech) {
		Alien alien = new Alien(aid,aname,tech);
		List<Course> course = repo1.findByCname(tech);
		alien.setFees(course.get(0).getFees());
		alien.setPaid(0);
		repo.save(alien);
		Alien alien1 = repo.findById(alien.getAid()).orElse(null);
		if(alien1==null) {
			return new ModelAndView("empty.jsp");
		}
		List<Alien> alien2 = new ArrayList<Alien>();
		alien2.add(alien1);
		ModelAndView mv = new ModelAndView("result.jsp","aliener",alien2);
		String s = "The New Student's Data added to the Database Successfully";
		mv.addObject("heading", s);
		return mv;
	}
	Request of Payment update:
	@RequestMapping("/paydetail")
	public ModelAndView paydetail(int aid) {
		Alien alien = repo.findById(aid).orElse(null);
		if(alien==null) {
			return new ModelAndView("empty.jsp");
		}
		int temp = alien.getFees()-alien.getPaid();
		if(temp==0) {
			return new ModelAndView("empty2.jsp"); 
		}
		payaid = alien.getAid();
		ModelAndView mv = new ModelAndView("paydetail.jsp","aliener",alien);
		mv.addObject("pend", temp);
		return mv;
	}
	
	@RequestMapping("/updatepay")
	public ModelAndView updatepay(int amt) {
		Alien alien = repo.findById(payaid).orElse(null);
		alien.setPaid(amt+alien.getPaid());
		repo.save(alien);
		payaid = 0;
ModelAndView mv = new ModelAndView("pay.jsp","heading","Payment Updated Successfully");
		return mv;
	}
Sample of some Test Cases:
	Test Case to test adding and updating student data:
	cc.addcres(course);
	ModelAndView mv = hc.add(102,"vignesh","java");
	String s = mv.getViewName();
	if(s.equals("result.jsp")) {
		Map<String, Object> m = mv.getModel();
		List<Alien> alien1 = (List<Alien>) m.get("aliener");
		assertEquals(alien.toString(), alien1.get(0).toString());
	}
		
alien.setAname("vikky");
	mv = hc.update1res(102,"vikky");
	s = mv.getViewName();
	if(s.equals("result.jsp")) {
		Map<String, Object> m = mv.getModel();
		List<Alien> alien1 = (List<Alien>) m.get("aliener");
		assertEquals(alien.toString(), alien1.get(0).toString());
	}
	Test Case to test updating payment detail:
	Alien alien = new Alien();	
	alien.setAid(102);
	alien.setAname("vignesh");
	alien.setTech("java");
	alien.setFees(12000);
	Course course = new Course();
	course.setCid(1);
	course.setCname("java");
	course.setDuration(12);
	course.setFees(12000);
	course.setTutor("John");
	cc.addcres(course);
	ModelAndView mv = hc.add(102,"vignesh","java");
	String s = mv.getViewName();
	if(s.equals("result.jsp")) {
		Map<String, Object> m = mv.getModel();
		List<Alien> alien1 = (List<Alien>) m.get("aliener");
		assertEquals(alien.toString(), alien1.get(0).toString());
	}
	mv = hc.paydetail(alien.getAid());
	s = mv.getViewName();
	if(s.equals("paydetail.jsp")) {
		Map<String, Object> m = mv.getModel();
		Alien alien1 = (Alien) m.get("aliener");
		assertEquals(alien.toString(), alien1.toString());
		int temp1 = (int) m.get("pend");
		assertEquals(alien.getFees(),temp1);
	}	
	hc.updatepay(1200);
	alien.setPaid(1200);
	mv = hc.get1res(102);
	s = mv.getViewName();
	if(s.equals("result.jsp")) {
		Map<String, Object> m = mv.getModel();
		List<Alien> alien1 = (List<Alien>) m.get("aliener");
		assertEquals(alien.toString(), alien1.get(0).toString());
	}
Installation Instruction:
1)	Download and Install Java SE Development 11 on your System from Official Oracle Website. https://www.oracle.com/java/technologies/javase-jdk11-downloads.html
2)	Download and Install Eclipse and Spring Tool Suite IDE from their Official Website. https://www.eclipse.org/downloads/packages/release/kepler/sr1/eclipse-ide-java-developers or https://spring.io/tools

How to run the Program:
1)	Download the code from github and Open the code in Eclipse or Spring Tool Suite IDE
2)	Run the Code as Java Application and Open http://localhost:8080/ in Your Browser to see the Output of Application.
3)	Run the Code as Java Application Tests to see the Output of test case.

Developer: thiyanesh@c1exchange.com
