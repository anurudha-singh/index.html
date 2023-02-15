# index.html
first web page
////reactive form implementation

import 'package:flutter/material.dart';
import 'package:reactive_forms/reactive_forms.dart';

class InvestIntro4 extends StatefulWidget {
  const InvestIntro4({Key? key}) : super(key: key);

  @override
  State<InvestIntro4> createState() => _InvestIntro4State();
}

class _InvestIntro4State extends State<InvestIntro4> {
  FormGroup buildForm() => fb.group(<String, Object>{
        'annualincome': FormControl<String>(
          validators: [Validators.required],
        ),
        'justme': false,
        'myhousehold': false
      });

  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
      child: ReactiveFormBuilder(
          form: buildForm,
          builder: (context, form, child) {
            return Container(
              margin: const EdgeInsets.all(10),
              child: Column(children: [
                Container(
                    margin: const EdgeInsets.all(20.0),
                    child: const Text(
                      "Typically, people put away 5% to 10% towards investing",
                      style: TextStyle(fontSize: 20.0),
                    )),
                SingleChildScrollView(
                  scrollDirection: Axis.horizontal,
                  child: Row(
                    children: [
                      const Text("Income", style: TextStyle(fontSize: 20.0)),
                      ReactiveCheckbox(formControlName: 'justme'),
                      const Text('Just Me', style: TextStyle(fontSize: 20.0)),
                      ReactiveCheckbox(formControlName: 'myhousehold'),
                      const Text(
                        "My HouseHold",
                        style: TextStyle(fontSize: 20.0),
                      ),
                    ],
                  ),
                ),
                SizedBox(
                  height: MediaQuery.of(context).size.height * 2 / 100,
                ),
                Container(
                  margin: const EdgeInsets.only(left: 100.0),
                  child: SizedBox(
                    width: MediaQuery.of(context).size.width * 60 / 100,
                    height: MediaQuery.of(context).size.height * 5 / 100,
                    child: ReactiveTextField<String>(
                      keyboardType: TextInputType.number,
                      formControlName: 'annualincome',
                      validationMessages: {
                        ValidationMessage.required: (_) =>
                            'The input value must not be empty',
                        ValidationMessage.number: (_) =>
                            'The input value should be in number format'
                      },
                      textInputAction: TextInputAction.next,
                      decoration: const InputDecoration(
                          hintText: "annual income",
                          border: OutlineInputBorder(
                              borderRadius:
                                  BorderRadius.all(Radius.circular(15.0)))),
                    ),
                  ),
                ),
                SizedBox(
                  height: MediaQuery.of(context).size.height * 5 / 100,
                ),
                Container(
                    margin: const EdgeInsets.only(left: 5.0),
                    child: const Text(
                      "Annual Savings     \$6000",
                      style: TextStyle(fontSize: 20.0),
                    )),
                SizedBox(
                  height: MediaQuery.of(context).size.height * 2 / 100,
                ),
                Container(
                    margin: const EdgeInsets.only(right: 30.0),
                    child: const Text(
                      "% of Income          6%",
                      style: TextStyle(fontSize: 20.0),
                    )),
                SizedBox(
                  height: MediaQuery.of(context).size.height * 10 / 100,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Container(
                        width: MediaQuery.of(context).size.width * 40 / 100,
                        decoration: BoxDecoration(
                          border: Border.all(
                            color: Colors.green,
                          ),
                          borderRadius: BorderRadius.circular(30.0),
                        ),
                        child: Container(
                          padding: const EdgeInsets.all(15.0),
                          child: const Center(
                              child: Text(
                            //adding alignemnt of text
                            textAlign: TextAlign.center,
                            "This is fine for now",
                            style: TextStyle(fontSize: 20.0),
                          )),
                        )),
                    SizedBox(
                      width: MediaQuery.of(context).size.width * 5 / 100,
                    ),
                    Container(
                        alignment: Alignment.center,
                        width: MediaQuery.of(context).size.width * 40 / 100,
                        decoration: BoxDecoration(
                          border: Border.all(
                            color: Colors.green,
                          ),
                          borderRadius: BorderRadius.circular(30.0),
                        ),
                        child: GestureDetector(
                          onTap: () {
                            // ignore: avoid_print
                            print(form.value);
                          },
                          child: Container(
                            padding: const EdgeInsets.all(15.0),
                            child: const Text(
                              "Set a new Target",
                              textAlign: TextAlign.center,
                              style: TextStyle(fontSize: 20.0),
                            ),
                          ),
                        ))
                  ],
                ),
              ]),
            );
          }),
    );
  }
}
