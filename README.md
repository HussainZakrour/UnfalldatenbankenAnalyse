from PyPDF2 import PdfReader
import os
import pandas as pd
import numpy as np
  
dir = "C:/Users/MONSTER/Desktop/Huss/repor"
report_data_frame = pd.DataFrame()
report_data_dict = {}
undone = []
  
for root, subdirs, files in sorted(os.walk(dir)):
    for file in files:
        if file.endswith(".pdf"):
            print('---------------------------------------------------------------------------------------------')
            try:
                pdf_reader = PdfReader(root + '/' + file)
                report_data_dict ["FILE_NAME"] = file
                for field_name, attributes in  pdf_reader.get_fields().items():
                    if '/V' in attributes:
                        field_value = attributes['/V']
                        #print(field_name ,field_value)
                        if field_name.find('WEATHER') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split() 
                                print('VEHICLE 1 ' + new_field_name[-1]+' WEATHER')
                                new_field_name = new_field_name[-1]+' WEATHER'
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split() 
                                print('VEHICLE 2 ' + new_field_name[-1]+' WEATHER')
                                new_field_name = new_field_name[-1]+' WEATHER'
                                field_name = new_field_name

                        if field_name.find('LIGHTING') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 1 ' + new_field_name[-1]+' LIGHTING')
                                new_field_name = new_field_name[-1]+' LIGHTING'
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 2 ' + new_field_name[-1]+' LIGHTING')
                                new_field_name = new_field_name[-1]+' LIGHTING'
                                field_name = new_field_name
                        if field_name.find('ROADWAY') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 1 ' + new_field_name[-1]+' ROADWAY')
                                new_field_name = new_field_name[-1]+' ROADWAY'
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 2 ' + new_field_name[-1]+' ROADWAY')
                                new_field_name = new_field_name[-1]+' ROADWAY'
                                field_name = new_field_name
                        if field_name.find('ROAD CONDITIONS') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 1 ' + new_field_name[-1]+' ROAD CONDITIONS')
                                new_field_name = new_field_name[-1]+' ROAD CONDITIONS'
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 2 ' + new_field_name[-1]+' ROAD CONDITIONS')
                                new_field_name = new_field_name[-1]+' ROAD CONDITIONS'
                                field_name = new_field_name
                        if field_name.find('MOVEMENT') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 1 ' + new_field_name[-1])
                                new_field_name = new_field_name[-1]
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 2 ' + new_field_name[-1])
                                new_field_name = new_field_name[-1]
                                field_name = new_field_name
                        if field_name.find('TYPE') != -1:
                            if attributes['/TU'].find('VEHICLE 1') != -1:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 1 ' + new_field_name[-1])
                                new_field_name = new_field_name[-1]
                                field_name = new_field_name
                            else:
                                new_field_name = attributes['/TU'].split('IF') 
                                print('VEHICLE 2 ' + new_field_name[-1])
                                new_field_name = new_field_name[-1]
                                field_name = new_field_name
                        if field_name.find('OTHER') != -1:
                            new_field_name = attributes['/TU'].split('IF') 
                            print('OTHER ' + new_field_name[-1])
                            new_field_name = new_field_name[-1]
                            field_name = new_field_name
                        report_data_dict[field_name] = field_value
                report_data_frame = report_data_frame.append(report_data_dict,ignore_index=True)
                                
            except Exception as e:
                print(e)
                undone.append(file)
          
          
report_data_frame

undone

csv_file_name = 'all_reports_dataset.xlsx'
report_data_frame.to_excel(csv_file_name)
          
         
