<?php
	class Report extends CI_Controller{
		function __construct()
		{
			parent::__construct();
			$this->load->helper('form');
			$this->load->helper('date');
			$this->load->helper('url');
			$this->load->helper('file');
			$this->load->library('email');
			$this->load->library('form_validation');
			$this->load->library('xml_writer');
			$this->config->load('report_def');
		}
	
		function index()
		{
			$data['date']=$this->config->item('date');
			$data['title']=$this->config->item('lb_title');
			$data['lb_cur']=$this->config->item('lb_cur');
			$data['lb_goals']=$this->config->item('lb_goals');
			$data['lb_hrs']=$this->config->item('lb_hrs');
			$data['lb_past']=$this->config->item('lb_past');
			$data['lb_ant']=$this->config->item('lb_ant');
			$data['lb_unt']=$this->config->item('lb_unt');
			$data['lb_mis']=$this->config->item('lb_mis');
			$data['lb_isu']=$this->config->item('lb_isu');
			$data['lb_sch']=$this->config->item('lb_sch');
			
			$data['to'] = $this->config->item('cfg_to');
			$data['from']=$this->config->item('from');
			$data['subject']=$data['title'].$data['date'];
			$data['main_content'] = 'report_form';
			$this->load->view('includes/template',$data);
		}
		function send()
		{
			
			$this->form_validation->set_rules('from', 'Email Address', 'trim|required|valid_email');
			$this->form_validation->set_rules('hours', 'Hours', 'trim|required|numeric');
			$this->form_validation->set_rules('mon', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('tue', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('wed', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('thu', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('fri', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('sat', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('sun', 'Hour Worked', 'trim|required|numeric');
			$this->form_validation->set_rules('tol', 'Hour Worked', 'trim|required|numeric');
			
			$data['title']=$this->config->item('lb_title');
			$data['lb_cur']=$this->config->item('lb_cur');
			$data['lb_goals']=$this->config->item('lb_goals');
			$data['lb_hrs']=$this->config->item('lb_hrs');
			$data['lb_past']=$this->config->item('lb_past');
			$data['lb_ant']=$this->config->item('lb_ant');
			$data['lb_unt']=$this->config->item('lb_unt');
			$data['lb_mis']=$this->config->item('lb_mis');
			$data['lb_isu']=$this->config->item('lb_isu');
			$data['lb_sch']=$this->config->item('lb_sch');
			
			$this->config->set_item('date',$this->input->post('date'));
			$data['date'] = $this->config->item('date');
			
			$data['from']=$this->input->post('from');
			$data['to']=$this->input->post('to');
			$data['subject']=$data['title'].$data['date'];
			
			$this->config->set_item('msg_goal',$this->input->post('goal'));
			$data['goal']=$this->config->item('msg_goal');
			$data['hrs']=$this->input->post('hours');
			$data['ant']=$this->input->post('lw_ant');
			$data['unt']=$this->input->post('lw_unt');
			$data['mis']=$this->input->post('lw_mis');
			$data['isu']=$this->input->post('issues');
			$hrs =array('Monday'=> $this->input->post('mon'),
						'Tuesday'=>$this->input->post('tue'),
						'Wednesday'=>$this->input->post('wed'),
						'Thursday'=>$this->input->post('thu'),
						'Friday '=>$this->input->post('fri'),
						'Saturday'=>$this->input->post('sat'),
						'Sunday'=>$this->input->post('sun'),
						'Total'=>$this->input->post('tol')
						);
			$data['note']=$this->input->post('note');
			
			if($this->form_validation->run()==FALSE)
			{
				//$data['main_content'] = 'report_form';
				//$this->load->view('includes/template',$data);
				echo validation_errors();
			}
			else
			{
				//Generating text message
				$msg = "";
				if ($data['note']){
					$msg = "\nNotes: \n".$data['note'];
					}
				$msg .= $data['lb_cur']."\n".
						$data['lb_goals']."\n".
							$data['goal']."\n\n".
						$data['lb_hrs']."\n".
							$data['hrs']."\n\n".
						$data['lb_past']."\n".
						$data['lb_ant']."\n".
							$data['ant']."\n\n".
						$data['lb_unt']."\n".
							$data['unt']."\n\n".
						$data['lb_mis']."\n".
							$data['mis']."\n\n".
						$data['lb_isu']."\n".
							$data['isu']."\n\n".
						$data['lb_sch']."\n";
							foreach($hrs as $day => $hr){
								if($hr>'0'){ $msg.=$day.": \t".$hr."\n"; }
							}
				//Generating XML
				$xml = new xml_writer;
				$xml->setRootName('WeeklyReport');
				$xml->initiate();
				$xml->startBranch('weekEnding-'.$data['date']);
					$xml->startBranch('thisWeek');
						$xml->startBranch('goals');
							$xml->addNode('goal', $data['goal']);
						$xml->endBranch();
						$xml->addNode('hours',$data['hrs']);
					$xml->endBranch();
					$xml->startBranch('lastWeek');
						$xml->startBranch('dones');
							$xml->addNode('done', $data['ant']);
						$xml->endBranch();
						$xml->startbranch('pluses');
							$xml->addNode('plus', $data['unt']);
						$xml->endBranch();
						$xml->startBranch('misses');
							$xml->addNode('miss', $data['mis']);
						$xml->endBranch();
					$xml->endBranch();
					$xml->startBranch('issues');
						$xml->addNode('issue', $data['isu']);
					$xml->endBranch();
					$xml->startBranch('didHours');
						foreach($hrs as $day => $hr){
							if($hr!='0'){ $xml->addNode(trim($day), trim($hr)); }
						}
					$xml->endBranch();
					$xml->startbranch('notes');
						$xml->addNode('note',$data['note']);
					$xml->endBranch();
				$xml->endBranch();
				
				$data['xml'] = $xml->getXml();
				
				if( !write_file($this->config->item('cfg_xmlPath'),$data['xml'], 'w+') ){
					$data['err'] = "Unable to write xml file <br/>";
				}
				else{ $data['err'] = 'Xml created <br/>'; }
				//echo symbolic_permissions(fileperms($this->config->item('cfg_xmlPath')));
				//echo octal_permissions(fileperms($this->config->item('cfg_xmlPath')));
				//echo print_r($this->input->post());
				
				$this->email->from($data['from']);
				$this->email->to($data['to']);
				$this->email->cc($data['from']);
				$this->email->subject($data['subject']);
				$this->email->message($msg);
				$this->email->attach($this->config->item('cfg_xmlPath'));
				
				$this->email->send();
				$data['main_content']='sent';
				$data['msg']=$this->email->print_debugger();
				
				$this->load->view('includes/template',$data);
			}
		}
	}
?>